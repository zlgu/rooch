
<a name="0x3_rooch_hash"></a>

# Module `0x3::rooch_hash`

Module which defines hash functions. Note that Sha-256 and Sha3-256 is available in the std::hash module in the
standard library.
Conflict with the standard library, change the name for hash


-  [Function `blake2b256`](#0x3_rooch_hash_blake2b256)
-  [Function `keccak256`](#0x3_rooch_hash_keccak256)


<pre><code></code></pre>



<a name="0x3_rooch_hash_blake2b256"></a>

## Function `blake2b256`

@param data: Arbitrary binary data to hash
Hash the input bytes using Blake2b-256 and returns 32 bytes.


<pre><code><b>public</b> <b>fun</b> <a href="rooch_hash.md#0x3_rooch_hash_blake2b256">blake2b256</a>(data: &<a href="">vector</a>&lt;u8&gt;): <a href="">vector</a>&lt;u8&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>native</b> <b>public</b> <b>fun</b> <a href="rooch_hash.md#0x3_rooch_hash_blake2b256">blake2b256</a>(data: &<a href="">vector</a>&lt;u8&gt;): <a href="">vector</a>&lt;u8&gt;;
</code></pre>



</details>

<a name="0x3_rooch_hash_keccak256"></a>

## Function `keccak256`

@param data: Arbitrary binary data to hash
Hash the input bytes using keccak256 and returns 32 bytes.


<pre><code><b>public</b> <b>fun</b> <a href="rooch_hash.md#0x3_rooch_hash_keccak256">keccak256</a>(data: &<a href="">vector</a>&lt;u8&gt;): <a href="">vector</a>&lt;u8&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>native</b> <b>public</b> <b>fun</b> <a href="rooch_hash.md#0x3_rooch_hash_keccak256">keccak256</a>(data: &<a href="">vector</a>&lt;u8&gt;): <a href="">vector</a>&lt;u8&gt;;
</code></pre>



</details>
