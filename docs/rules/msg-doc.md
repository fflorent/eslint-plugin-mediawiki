[//]: # (This file is generated by eslint-docgen. Do not edit it directly.)

# msg-doc

Ensures message keys are documented when they are constructed.

📋 This rule is enabled in `plugin:mediawiki/common`.

## Rule details

❌ Examples of **incorrect** code:
```js
message = mw.msg( 'foo-' + bar );
message = mw.msg( cond ? 'baz' : 'foo-' + bar );

// This can produce:
// * foo-bar-baz
message = mw.msg( 'foo-' + bar );

// This can produce:
// * foo-bar-baz
// * foo-bar-baz
message = mw.msg( 'foo-' + bar );

// This constructs foo-baz or foo-quux
message = mw.msg( 'foo-' + bar );

/**
 The following messages are used here:
 * foo-baz
 * foo-quux
 */
display( mw.msg( 'foo-' + bar ), baz );

function foo() {
    const first = mw.msg( 'foo-' + baz ),
        // This can produce:
        // * bar-x
        // * bar-y
        second = mw.msg( 'bar-' + baz );
}

function foo() {
    const
        // This can produce:
        // * foo-x
        // * foo-y
        first = mw.msg( 'foo-' + baz ),
        second = mw.msg( 'bar-' + baz );
}

function foo() {
    // This can produce:
    // * foo-x
    // * foo-y
    const first = mw.msg( 'foo-' + baz ),
        second = mw.msg( 'bar-' + baz );
}

function foo() {
    let first = mw.msg( 'foo-' + baz ), second;
    bar.quux();
    // This can produce:
    // * bar-x
    // * bar-y
    second = mw.msg( 'bar-' + baz );
}
```

✔️ Examples of **correct** code:
```js
// The following messages are used here:
// * foo-baz
// * foo-quux
display( mw.msg( 'foo-' + bar ), baz );

// The following messages are used here:
// * foo-baz
// * foo-quux
// * foo-whee
message = mw.msg( 'foo-' + bar );

$foo
    // The following messages are used here:
    // * foo-baz
    // * foo-quux
    .text( mw.msg( 'foo-' + bar ) );

function foo() {
    const
        // This can produce:
        // * foo-x
        // * foo-y
        first = mw.msg( 'foo-' + baz ),
        // This can produce:
        // * bar-x
        // * bar-y
        second = mw.msg( 'bar-' + baz );
}

function foo() {
    // This can produce:
    // * foo-x
    // * foo-y
    const first = mw.msg( 'foo-' + baz ),
        // This can produce:
        // * bar-x
        // * bar-y
        second = mw.msg( 'bar-' + baz );
}

message = mw.msg( test ? 'foo' : 'bar' );
message = mw.msg( test ? ( test2 ? 'foo' : 'bar' ) : ( test2 ? 'baz' : 'quux' ) );
message = mw.msg( 'foo-bar' );
message = mw.message( 'foo-bar' ).plain();
message = OO.ui.deferMsg( 'foo-bar' );
message = ve.msg( 'foo-bar' );
message = mw.msg();
```

## Resources

* [Rule source](/src/rules/msg-doc.js)
* [Test source](/tests/rules/msg-doc.js)
