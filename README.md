# File::LibMagic::FFI

Determine MIME types of data or files using libmagic

# SYNOPSIS

    use File::LibMagic;
    
    my $magic = File::LibMagic->new;
    
    # prints a description like "ASCII text"
    say $magic->describe_filename('path/to/file');
    say $magic->describe_contents('this is some data');
    
    # Prints a MIME type like "text/plain; charset=us-ascii"
    say $magic->checktype_filename('path/to/file');
    say $magic->checktype_contents('this is some data');

# DESCRIPTION

This module is a simple Perl interface to `libmagic`.  It provides the same full undeprecated interface as [File::LibMagic](https://metacpan.org/pod/File::LibMagic), but it uses [FFI::Raw](https://metacpan.org/pod/FFI::Raw) instead of `XS` for
its implementation, and thus can be used without a compiler.

# API

This module provides an object-oriented API with the following methods:

## new

    my $magic = File::LibMagic->new;
    my $magic = File::LibMagic->new('/etc/magic');

Creates a new File::LibMagic::FFI object.

Using the object oriented interface provides an efficient way to repeatedly determine the magic of a file.

This method takes an optional argument containing a path to the magic file.  If the file doesn't exist, this will throw an exception.

If you don't pass an argument, it will throw an exception if it can't find any magic files at all.

## checktype\_contents

    my $mime_type = $magic->checktype_contents($data);

Returns the MIME type of the data given as the first argument.  The data can be passed as a plain scalar or as a reference to a scalar.

This is the same value as would be returned by the `file` command with the `-i` option.

## checktype\_filename

    my $mime_type = $magic->checktype_filename($filename);

Returns the MIME type of the given file.

This is the same value as would be returned by the `file` command with the `-i` option.

## describe\_contents

    my $description = $magic->describe_contents($data);

Returns a description (as a string) of the data given as the first argument. The data can be passed as a plain scalar or as a reference to a scalar.

This is the same value as would be returned by the `file` command with no options.

## describe\_filename

    my $description = $magic->describe_filename($filename);

Returns a description (as a string) of the given file.

This is the same value as would be returned by the `file` command with no options.

# DEPRECATED APIS

The FFI version does not support the deprecated APIs that [File::LibMagic](https://metacpan.org/pod/File::LibMagic) does.

## SEE ALSO

- [File::LibMagic](https://metacpan.org/pod/File::LibMagic)
- [FFI::Raw](https://metacpan.org/pod/FFI::Raw)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2014 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
