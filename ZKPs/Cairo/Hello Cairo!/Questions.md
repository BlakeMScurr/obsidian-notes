What is going on with apparent writeable memory here? https://www.cairo-lang.org/docs/hello_cairo/amm.html#computing-the-merkle-roots
```
let res = account.public_key
let (res) = hash2{hash_ptr=pedersen_ptr}(
	res, account.token_a_balance)
let (res) = hash2{hash_ptr=pedersen_ptr}(
	res, account.token_b_balance)
return (res=res)
```
It looks like we're rewriting the value of res! But memory in cairo is supposed to be immutable, that's the point of the dict_access stuff! Is it that we can write over memory, and it implicitly creates a new value and hides the old one? But why can't we do the same thing for dictionaries? Is it that we need to prove integrity and continual updates for each key?

Also, wtf is going on with `small_merkle_tree` returning two roots? 
```
let (root_before, root_after) = small_merkle_tree{
	hash_ptr=pedersen_ptr}(
	squashed_dict_start=hash_dict_start,
	squashed_dict_end=hash_dict_end,
	height=LOG_N_ACCOUNTS)
```