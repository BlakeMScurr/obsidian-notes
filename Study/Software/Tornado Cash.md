#flashcards/software/tornado_cash

# Outline

How do deposits work?
?
The user privately generates random bytes, hashes them, and sends them to the contract.
The user also sends the token.
The contract inserts the hash into a Merkle Tree.
<!--SR:2022-06-21,13,250-->

How do withdrawls work?
?
The user splits their private note into a secret part and a nullifier.
The user generates a zkp of the merkle proof that their nullifier is in the tree.
The user sends the nullifier and the zkp to the contract who verifies it and sends the user money.
<!--SR:2022-06-16,11,250-->

What are the circom files in tornado cash?
?
withdraw.circom and merkleTree.circom
<!--SR:2022-06-17,12,250-->

## Withdraw

What does withdraw.circom include?
?
circomlib/circuits/bitify.circom
circomlib/circuits/pedersen.circom
merkleTree.circom
<!--SR:2022-06-13,7,210-->

## MerkleTree

What does merkleTree.circom include?
?
circomlib/circuits/mimcsponge.circom
<!--SR:2022-06-13,8,230-->

What are the top level constructions in merkleTree.circom?
?
The HashLeftRight template
The DualMux template
The MerkleTreeChecker template
<!--SR:2022-06-14,7,190-->

What does HashLeftRight do?
?
Outputs the mimcsponge hash of two input signals left and right.
I.e., `computes MiMC([left, right])`
<!--SR:2022-06-18,12,250-->

What is the code for HashLeftRight?
?
```
template HashLeftRight(){
	input signal left;
	input signal right;
	output signal out;
	
	component mimc = MiMCSponge(2, 1);
	mimc.ins[0] <== left;
	mimc.ins[1] <== right;
	mimc.k <== 0;
	out <== mimc.outs[0];
}
```
<!--SR:2022-06-12,6,210-->

What does DualMux do?
?
if `s === 0` returns `[in[0], in[1]]`
if `s === 1` returns `[in[1], in[0]]`
<!--SR:2022-06-17,12,250-->

What is the code for DualMux?
?
```
template DualMux(){
	input signal in[2];
	input signal s;
	output signal out[2];
	s * (s-1) === 0;
	out[0] <== (in[1] - in[0]) * s + in[0];
	out[1] <== (in[0] - in[1]) * s + in[1];
}
```
<!--SR:2022-06-14,10,250-->





