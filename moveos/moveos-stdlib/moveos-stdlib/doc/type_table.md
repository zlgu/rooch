
<a name="0x2_type_table"></a>

# Module `0x2::type_table`

TypeTable is a table use struct Type as Key, struct as Value


-  [Struct `TypeTable`](#0x2_type_table_TypeTable)
-  [Function `new`](#0x2_type_table_new)
-  [Function `new_with_id`](#0x2_type_table_new_with_id)
-  [Function `add`](#0x2_type_table_add)
-  [Function `add_internal`](#0x2_type_table_add_internal)
-  [Function `borrow`](#0x2_type_table_borrow)
-  [Function `borrow_internal`](#0x2_type_table_borrow_internal)
-  [Function `borrow_mut`](#0x2_type_table_borrow_mut)
-  [Function `borrow_mut_internal`](#0x2_type_table_borrow_mut_internal)
-  [Function `remove`](#0x2_type_table_remove)
-  [Function `remove_internal`](#0x2_type_table_remove_internal)
-  [Function `contains`](#0x2_type_table_contains)
-  [Function `contains_internal`](#0x2_type_table_contains_internal)
-  [Function `destroy`](#0x2_type_table_destroy)


<pre><code><b>use</b> <a href="">0x1::ascii</a>;
<b>use</b> <a href="">0x1::type_name</a>;
<b>use</b> <a href="object_id.md#0x2_object_id">0x2::object_id</a>;
<b>use</b> <a href="raw_table.md#0x2_raw_table">0x2::raw_table</a>;
<b>use</b> <a href="tx_context.md#0x2_tx_context">0x2::tx_context</a>;
</code></pre>



<a name="0x2_type_table_TypeTable"></a>

## Struct `TypeTable`



<pre><code><b>struct</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>handle: <a href="object_id.md#0x2_object_id_ObjectID">object_id::ObjectID</a></code>
</dt>
<dd>

</dd>
</dl>


</details>

<a name="0x2_type_table_new"></a>

## Function `new`

Create a new Table.


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_new">new</a>(ctx: &<b>mut</b> <a href="tx_context.md#0x2_tx_context_TxContext">tx_context::TxContext</a>): <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_new">new</a>(ctx: &<b>mut</b> TxContext): <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a> {
    <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a> {
        handle: <a href="raw_table.md#0x2_raw_table_new_table_handle">raw_table::new_table_handle</a>(ctx),
    }
}
</code></pre>



</details>

<a name="0x2_type_table_new_with_id"></a>

## Function `new_with_id`

Create a new Table with a given handle.


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_new_with_id">new_with_id</a>(handle: <a href="object_id.md#0x2_object_id_ObjectID">object_id::ObjectID</a>): <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_new_with_id">new_with_id</a>(handle: ObjectID): <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>{
    <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a> {
        handle,
    }
}
</code></pre>



</details>

<a name="0x2_type_table_add"></a>

## Function `add`

Add a new entry to the table. Aborts if an entry for this
key already exists. The entry itself is not stored in the
table, and cannot be discovered from it.


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_add">add</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>, val: V)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_add">add</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>, val: V) {
    <a href="type_table.md#0x2_type_table_add_internal">add_internal</a>&lt;V&gt;(<a href="table.md#0x2_table">table</a>, val)
}
</code></pre>



</details>

<a name="0x2_type_table_add_internal"></a>

## Function `add_internal`



<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_add_internal">add_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>, val: V)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_add_internal">add_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>, val: V) {
    <a href="raw_table.md#0x2_raw_table_add">raw_table::add</a>&lt;String, V&gt;(&<a href="table.md#0x2_table">table</a>.handle, <a href="type_table.md#0x2_type_table_key">key</a>&lt;V&gt;(), val)
}
</code></pre>



</details>

<a name="0x2_type_table_borrow"></a>

## Function `borrow`

Acquire an immutable reference to the value which <code>key</code> maps to.
Aborts if there is no entry for <code>key</code>.


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_borrow">borrow</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): &V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_borrow">borrow</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): &V {
    <a href="type_table.md#0x2_type_table_borrow_internal">borrow_internal</a>&lt;V&gt;(<a href="table.md#0x2_table">table</a>)
}
</code></pre>



</details>

<a name="0x2_type_table_borrow_internal"></a>

## Function `borrow_internal`



<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_borrow_internal">borrow_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): &V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_borrow_internal">borrow_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): &V {
    <a href="raw_table.md#0x2_raw_table_borrow">raw_table::borrow</a>&lt;String, V&gt;(&<a href="table.md#0x2_table">table</a>.handle, <a href="type_table.md#0x2_type_table_key">key</a>&lt;V&gt;())
}
</code></pre>



</details>

<a name="0x2_type_table_borrow_mut"></a>

## Function `borrow_mut`

Acquire a mutable reference to the value which <code>key</code> maps to.
Aborts if there is no entry for <code>key</code>.


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_borrow_mut">borrow_mut</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): &<b>mut</b> V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_borrow_mut">borrow_mut</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): &<b>mut</b> V {
    <a href="type_table.md#0x2_type_table_borrow_mut_internal">borrow_mut_internal</a>&lt;V&gt;(<a href="table.md#0x2_table">table</a>)
}
</code></pre>



</details>

<a name="0x2_type_table_borrow_mut_internal"></a>

## Function `borrow_mut_internal`



<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_borrow_mut_internal">borrow_mut_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): &<b>mut</b> V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_borrow_mut_internal">borrow_mut_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): &<b>mut</b> V {
    <a href="raw_table.md#0x2_raw_table_borrow_mut">raw_table::borrow_mut</a>&lt;String, V&gt;(&<a href="table.md#0x2_table">table</a>.handle, <a href="type_table.md#0x2_type_table_key">key</a>&lt;V&gt;())
}
</code></pre>



</details>

<a name="0x2_type_table_remove"></a>

## Function `remove`

Remove from <code><a href="table.md#0x2_table">table</a></code> and return the value which <code>key</code> maps to.
Aborts if there is no entry for <code>key</code>.


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_remove">remove</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_remove">remove</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): V {
    <a href="type_table.md#0x2_type_table_remove_internal">remove_internal</a>&lt;V&gt;(<a href="table.md#0x2_table">table</a>)
}
</code></pre>



</details>

<a name="0x2_type_table_remove_internal"></a>

## Function `remove_internal`



<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_remove_internal">remove_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_remove_internal">remove_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<b>mut</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): V {
    <a href="raw_table.md#0x2_raw_table_remove">raw_table::remove</a>&lt;String, V&gt;(&<a href="table.md#0x2_table">table</a>.handle, <a href="type_table.md#0x2_type_table_key">key</a>&lt;V&gt;())
}
</code></pre>



</details>

<a name="0x2_type_table_contains"></a>

## Function `contains`

Returns true if <code><a href="table.md#0x2_table">table</a></code> contains an entry for <code>key</code>.


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_contains">contains</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="type_table.md#0x2_type_table_contains">contains</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): bool {
    <a href="raw_table.md#0x2_raw_table_contains">raw_table::contains</a>&lt;String&gt;(&<a href="table.md#0x2_table">table</a>.handle, <a href="type_table.md#0x2_type_table_key">key</a>&lt;V&gt;())
}
</code></pre>



</details>

<a name="0x2_type_table_contains_internal"></a>

## Function `contains_internal`



<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_contains_internal">contains_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_contains_internal">contains_internal</a>&lt;V: key&gt;(<a href="table.md#0x2_table">table</a>: &<a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>): bool {
    <a href="raw_table.md#0x2_raw_table_contains">raw_table::contains</a>&lt;String&gt;(&<a href="table.md#0x2_table">table</a>.handle, <a href="type_table.md#0x2_type_table_key">key</a>&lt;V&gt;())
}
</code></pre>



</details>

<a name="0x2_type_table_destroy"></a>

## Function `destroy`

TODO should open the destroy function to public?


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_destroy">destroy</a>(<a href="table.md#0x2_table">table</a>: <a href="type_table.md#0x2_type_table_TypeTable">type_table::TypeTable</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(<b>friend</b>) <b>fun</b> <a href="type_table.md#0x2_type_table_destroy">destroy</a>(<a href="table.md#0x2_table">table</a>: <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>) {
    <b>let</b> <a href="type_table.md#0x2_type_table_TypeTable">TypeTable</a>{handle} = <a href="table.md#0x2_table">table</a>;
    <a href="raw_table.md#0x2_raw_table_destroy">raw_table::destroy</a>(&handle)
}
</code></pre>



</details>
