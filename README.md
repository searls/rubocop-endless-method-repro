# Rubocop and endless methods

Running:

```
$ ruby -v
ruby 2.7.2p137 (2020-10-01 revision 5445e04352) [x86_64-darwin20]
$ rubocop -v
1.8.1
```

And executing this:

```
$ echo "def Foo;'hi'end" | bundle exec rubocop -a -s wat.rb
```

Results in:

```
Inspecting 1 file
E

Offenses:

wat.rb:1:1: C: [Corrected] Style/SingleLineMethods: Avoid single-line method definitions.
def Foo;'hi'end
^^^^^^^^^^^^^^^
wat.rb:1:8: C: [Corrected] Layout/SpaceAfterSemicolon: Space missing after semicolon.
def Foo;'hi'end
       ^
wat.rb:1:11: E: Lint/Syntax: unexpected token tEQL
(Using Ruby 2.4 parser; configure using TargetRubyVersion parameter, under AllCops)
def Foo() = 'hi'
          ^

1 file inspected, 3 offenses detected, 2 offenses corrected
====================
def Foo() = 'hi'
```

Seems bad, since:

```
$ ruby -e "def Foo() = 'hi'"
```

Fails with:

```
-e:1: syntax error, unexpected '='
def Foo() = 'hi'
-e:1: syntax error, unexpected end-of-input, expecting `end'
```
