## PeterO.URIUtility

    public static class URIUtility

Contains utility methods for processing Uniform Resource Identifiers (URIs) and Internationalized Resource Identifiers (IRIs) under RFC3986 and RFC3987, respectively. In the following documentation, URIs and IRIs include URI references and IRI references, for convenience. There are five components to a URI: scheme, authority, path, query, and fragment identifier. The generic syntax to these components is defined in RFC3986 and extended in RFC3987. According to RFC3986, different URI schemes can further restrict the syntax of the authority, path, and query component (see also RFC 7320). However, the syntax of fragment identifiers depends on the media type (also known as MIME type) of the resource a URI references (see also RFC 3986 and RFC 7320). As of September 3, 2019, only the following media types specify a syntax for fragment identifiers:

 * The following application/* media types: epub+zip, pdf, senml+cbor, senml+json, senml-exi, sensml+cbor, sensml+json, sensml-exi, smil, vnd.3gpp-v2x-local-service-information, vnd.3gpp.mcdata-signalling, vnd.collection.doc+json, vnd.hc+json, vnd.hyper+json, vnd.hyper-item+json, vnd.mason+json, vnd.microsoft.portable-executable, vnd.oma.bcast.sgdu, vnd.shootproof+json

 * The following image/* media types: avci, avcs, heic, heic-sequence, heif, heif-sequence, hej2k, hsj2, jxra, jxrs, jxsi, jxss

 * The XML media types: application/xml, application/xml-external-parsed-entity, text/xml, text/xml-external-parsed-entity, application/xml-dtd

 * All media types with subtypes ending in "+xml" (see RFC 7303) use XPointer Framework syntax as fragment identifiers, except the following application/* media types: dicom+xml (syntax not defined), senml+xml (own syntax), sensml+xml (own syntax), ttml+xml (own syntax), xliff+xml (own syntax), yang-data+xml (syntax not defined)

 * font/collection

 * multipart/x-mixed-replace

 * text/plain

 * text/csv

 * text/html

 * text/markdown

 * text/vnd.a

### Member Summary
* <code>[BuildIRI(string, string, string, string)](#BuildIRI_string_string_string_string)</code> - Builds an internationalized resource identifier (IRI) from its components.
* <code>[DirectoryPath(string)](#DirectoryPath_string)</code> - Extracts the scheme, the authority, and the path component (up to and including the last "/" in the path if any) from the given URI or IRI, using the IRIStrict parse mode to check the URI or IRI.
* <code>[DirectoryPath(string, PeterO.ParseMode)](#DirectoryPath_string_PeterO_ParseMode)</code> -
* <code>[EncodeStringForURI(string)](#EncodeStringForURI_string)</code> - Encodes characters other than "unreserved" characters for URIs.
* <code>[EscapeURI(string, int)](#EscapeURI_string_int)</code> - Escapes characters that can't appear in URIs or IRIs.
* <code>[HasScheme(string)](#HasScheme_string)</code> - Determines whether the string is a valid IRI with a scheme component.
* <code>[HasSchemeForURI(string)](#HasSchemeForURI_string)</code> - Determines whether the string is a valid URI with a scheme component.
* <code>[IsValidCurieReference(string, int, int)](#IsValidCurieReference_string_int_int)</code> - Determines whether the substring is a valid CURIE reference under RDFA 1.
* <code>[IsValidIRI(string)](#IsValidIRI_string)</code> - Returns whether a string is a valid IRI according to the IRIStrict parse mode.
* <code>[IsValidIRI(string, PeterO.ParseMode)](#IsValidIRI_string_PeterO_ParseMode)</code> -
* <code>[PercentDecode(string)](#PercentDecode_string)</code> - Decodes percent-encoding (of the form "%XX" where X is a hexadecimal digit) in the given string.
* <code>[PercentDecode(string, int, int)](#PercentDecode_string_int_int)</code> - Decodes percent-encoding (of the form "%XX" where X is a hexadecimal digit) in the given portion of a string.
* <code>[RelativeResolve(string, string)](#RelativeResolve_string_string)</code> - Resolves a URI or IRI relative to another URI or IRI.
* <code>[RelativeResolve(string, string, PeterO.ParseMode)](#RelativeResolve_string_string_PeterO_ParseMode)</code> -
* <code>[RelativeResolveWithinBaseURI(string, string)](#RelativeResolveWithinBaseURI_string_string)</code> - Resolves a URI or IRI relative to another URI or IRI, but only if the resolved URI has no ".
* <code>[SplitIRI(string)](#SplitIRI_string)</code> - Parses an Internationalized Resource Identifier (IRI) reference under RFC3987.
* <code>[SplitIRI(string, int, int, PeterO.ParseMode)](#SplitIRI_string_int_int_PeterO_ParseMode)</code> -
* <code>[SplitIRI(string, PeterO.ParseMode)](#SplitIRI_string_PeterO_ParseMode)</code> -
* <code>[SplitIRIToStrings(string)](#SplitIRIToStrings_string)</code> - Parses an Internationalized Resource Identifier (IRI) reference under RFC3987.

<a id="BuildIRI_string_string_string_string"></a>
### BuildIRI

    public static string BuildIRI(
        string schemeAndAuthority,
        string path,
        string query,
        string fragment);

Builds an internationalized resource identifier (IRI) from its components.

<b>Parameters:</b>

 * <i>schemeAndAuthority</i>: String representing a scheme component, an authority component, or both. Examples of this parameter include "example://example", "example:", and "//example", but not "example". Can be null or empty.

 * <i>path</i>: A string representing a path component. Can be null or empty.

 * <i>query</i>: The query string. Can be null or empty.

 * <i>fragment</i>: The fragment identifier. Can be null or empty.

<b>Return Value:</b>

A URI built from the given components.

<b>Exceptions:</b>

 * System.ArgumentException:
Invalid schemeAndAuthority parameter, or the arguments result in an invalid IRI.

<a id="DirectoryPath_string"></a>
### DirectoryPath

    public static string DirectoryPath(
        string uri);

Extracts the scheme, the authority, and the path component (up to and including the last "/" in the path if any) from the given URI or IRI, using the IRIStrict parse mode to check the URI or IRI. Any "./" or "../" in the path is not condensed.

<b>Parameters:</b>

 * <i>uri</i>: A text string representing a URI or IRI. Can be null.

<b>Return Value:</b>

The directory path of the URI or IRI. Returns null if "uri" is null or not a valid URI or IRI.

<b>Exceptions:</b>

 * System.ArgumentNullException:
The parameter  <i>uri</i>
 is null.

<a id="EncodeStringForURI_string"></a>
### EncodeStringForURI

    public static string EncodeStringForURI(
        string s);

Encodes characters other than "unreserved" characters for URIs.

<b>Parameters:</b>

 * <i>s</i>: A string to encode.

<b>Return Value:</b>

The encoded string.

<b>Exceptions:</b>

 * System.ArgumentNullException:
The parameter  <i>s</i>
 is null.

<a id="EscapeURI_string_int"></a>
### EscapeURI

    public static string EscapeURI(
        string s,
        int mode);

Escapes characters that can't appear in URIs or IRIs. The function is idempotent; that is, calling the function again on the result with the same mode doesn't change the result.

<b>Parameters:</b>

 * <i>s</i>: A string to escape.

 * <i>mode</i>:  Has the following meaning: 0 = Encode reserved code points, code points below U+0021, code points above U+007E, and square brackets within the authority component, and do the IRISurrogateLenient check. 1 = Encode code points above U+007E, and square brackets within the authority component, and do the IRIStrict check. 2 = Same as 1, except the check is IRISurrogateLenient. 3 = Same as 0, except that percent characters that begin illegal percent-encoding are also encoded.

<b>Return Value:</b>

A string possibly containing escaped characters, or null if s is null.

<a id="HasScheme_string"></a>
### HasScheme

    public static bool HasScheme(
        string refValue);

Determines whether the string is a valid IRI with a scheme component. This can be used to check for relative IRI references. The following cases return true:

    xx-x:mm example:/ww

 The following cases return false:

    x@y:/z /x/y/z example.xyz

 .

<b>Parameters:</b>

 * <i>refValue</i>: A string representing an IRI to check.

<b>Return Value:</b>

 `true`  if the string is a valid IRI with a scheme component; otherwise,  `false`  .

<a id="HasSchemeForURI_string"></a>
### HasSchemeForURI

    public static bool HasSchemeForURI(
        string refValue);

Determines whether the string is a valid URI with a scheme component. This can be used to check for relative URI references. The following cases return true:

    http://example/z xx-x:mm example:/ww

 The following cases return false:

    x@y:/z /x/y/z example.xyz

 .

<b>Parameters:</b>

 * <i>refValue</i>: A string representing an IRI to check.

<b>Return Value:</b>

 `true`  if the string is a valid URI with a scheme component; otherwise,  `false`  .

<a id="IsValidCurieReference_string_int_int"></a>
### IsValidCurieReference

    public static bool IsValidCurieReference(
        string s,
        int offset,
        int length);

Determines whether the substring is a valid CURIE reference under RDFA 1.1. (The CURIE reference is the part after the colon.).

<b>Parameters:</b>

 * <i>s</i>: A string containing a CURIE reference. Can be null.

 * <i>offset</i>: A Index starting at 0 showing where the desired portion of "s" begins.

 * <i>length</i>: The number of elements in the desired portion of "s" (but not more than "s" 's length).

<b>Return Value:</b>

 `true`  if the substring is a valid CURIE reference under RDFA 1; otherwise,  `false`  . Returns false if  <i>s</i>
 is null.

<b>Exceptions:</b>

 * System.ArgumentException:
Either  <i>offset</i>
 or  <i>length</i>
 is less than 0 or greater than  <i>s</i>
 's length, or  <i>s</i>
 ' s length minus  <i>offset</i>
 is less than  <i>length</i>
 .

 * System.ArgumentNullException:
The parameter  <i>s</i>
 is null.

<a id="IsValidIRI_string"></a>
### IsValidIRI

    public static bool IsValidIRI(
        string s);

Returns whether a string is a valid IRI according to the IRIStrict parse mode.

<b>Parameters:</b>

 * <i>s</i>: A text string. Can be null.

<b>Return Value:</b>

True if the string is not null and is a valid IRI; otherwise, false.

<a id="PercentDecode_string"></a>
### PercentDecode

    public static string PercentDecode(
        string str);

Decodes percent-encoding (of the form "%XX" where X is a hexadecimal digit) in the given string. Successive percent-encoded bytes are assumed to form characters in UTF-8.

<b>Parameters:</b>

 * <i>str</i>: A string that may contain percent encoding. May be null.

<b>Return Value:</b>

The string in which percent-encoding was decoded.

<a id="PercentDecode_string_int_int"></a>
### PercentDecode

    public static string PercentDecode(
        string str,
        int index,
        int endIndex);

Decodes percent-encoding (of the form "%XX" where X is a hexadecimal digit) in the given portion of a string. Successive percent-encoded bytes are assumed to form characters in UTF-8.

<b>Parameters:</b>

 * <i>str</i>: A string a portion of which may contain percent encoding. May be null.

 * <i>index</i>: Index starting at 0 showing where the desired portion of  <i>str</i>
 begins.

 * <i>endIndex</i>: Index starting at 0 showing where the desired portion of  <i>str</i>
 ends. The character before this index is the last character.

<b>Return Value:</b>

The portion of the given string in which percent-encoding was decoded. Returns null if  <i>str</i>
 is ull.

<a id="RelativeResolve_string_string"></a>
### RelativeResolve

    public static string RelativeResolve(
        string refValue,
        string baseURI);

Resolves a URI or IRI relative to another URI or IRI.

<b>Parameters:</b>

 * <i>refValue</i>: A string representing a URI or IRI reference. Example:  `dir/file.txt`  .

 * <i>baseURI</i>: A string representing an absolute URI reference. Example:  `http://example.com/my/path/`  .

<b>Return Value:</b>

The resolved IRI, or null if  <i>refValue</i>
 is null or is not a valid IRI. If  <i>baseURI</i>
 is null or is not a valid IRI, returns refValue. Example:  `http://example.com/my/path/dir/file.txt`  .

<a id="RelativeResolveWithinBaseURI_string_string"></a>
### RelativeResolveWithinBaseURI

    public static string RelativeResolveWithinBaseURI(
        string refValue,
        string absoluteBaseURI);

Resolves a URI or IRI relative to another URI or IRI, but only if the resolved URI has no "." or ".." component in its path and only if resolved URI's directory path matches that of the second URI or IRI.

<b>Parameters:</b>

 * <i>refValue</i>: A string representing a URI or IRI reference. Example:  `dir/file.txt`  .

 * <i>absoluteBaseURI</i>: A string representing an absolute URI reference. Example:  `http://example.com/my/path/`  .

<b>Return Value:</b>

The resolved IRI, or null if  <i>refValue</i>
 is null or is not a valid IRI, or  <i>refValue</i>
 if  <i>absoluteBaseURI</i>
 is null or an empty string, or null if "absoluteBaseURI" is neither null nor empty and is not a valid IRI. Returns null instead if the resolved IRI has no "." or ".." component in its path or if the resolved URI's directory path does not match that of "absoluteBaseURI". Example:  `http://example.com/my/path/dir/file.txt`  .

<a id="SplitIRI_string"></a>
### SplitIRI

    public static int[] SplitIRI(
        string s);

Parses an Internationalized Resource Identifier (IRI) reference under RFC3987. If the IRI reference is syntactically valid, splits the string into its components and returns an array containing the indices into the components.

<b>Parameters:</b>

 * <i>s</i>: A string that contains an IRI. Can be null.

<b>Return Value:</b>

If the string is a valid IRI reference, returns an array of 10 integers. Each of the five pairs corresponds to the start and end index of the IRI's scheme, authority, path, query, or fragment identifier, respectively. The scheme, authority, query, and fragment identifier, if present, will each be given without the ending colon, the starting "//", the starting "?", and the starting "#", respectively. If a component is absent, both indices in that pair will be -1. If the string is null or is not a valid IRI, returns null.

<a id="SplitIRIToStrings_string"></a>
### SplitIRIToStrings

    public static string[] SplitIRIToStrings(
        string s);

Parses an Internationalized Resource Identifier (IRI) reference under RFC3987. If the IRI reference is syntactically valid, splits the string into its components and returns an array containing those components.

<b>Parameters:</b>

 * <i>s</i>: A string that contains an IRI. Can be null.

<b>Return Value:</b>

If the string is a valid IRI reference, returns an array of five strings. Each of the five pairs corresponds to the IRI's scheme, authority, path, query, or fragment identifier, respectively. If a component is absent, the corresponding element will be null. If the string is null or is not a valid IRI, returns null.