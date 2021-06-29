# Chapter 1
## What Is XML?
- XML (eXtensible Markup Language ) is a metalanguage for defining vocabularies. XML-based vocabularies let you describe documents in a meaningful way.
- XML vocabulary documents are text-based and consist of markup and content. Markup is evidenced via tagsand each tag has a name (Ex: <ingredients> ... </ingredients>). Furthermore, some tags have attribute (Ex: <ingredient qty="2"> ... </ingredient>).
- Has user-custom tags intead of pre-definned tags like HTML.
## Language Features
## XML Declaration
- An XML document usually begins with the XML declaration, which is special markup telling an XML parser that the document is XML. The absence of the XML declaration in Listing 1-1 reveals that this special markup isn’t mandatory. When the XML declaration is present, nothing can appear before it.
- Ex: <?xml version="1.0" encoding="ISO-8859-1"?>
- XML supports Unicode, which means that XML documents consist entirely of characters taken from the Unicode character set. The document’s characters are encoded into bytes for storage or transmission, and the encoding is specified via the XML declaration’s optional encoding attribute.
- The final attribute that can appear in the XML declaration is standalone. This optional attribute, which is only relevant with DTDs, determines if there are external markup declarationsthat affect the information passed from an XML processor (a parser) to the application. Its value defaults to no, implying that there are, or maybe, such declarations. A yes value indicates that there are no such declarations.
### Elements and Attributes
- XML has a hierarchical structure of elements, where an element is a portion of the document delimited by a start tag (such as <name>) and an end tag (such as </name>), or is an empty-element tag (a standalone tag whose name ends with a forward slash ( /), such as <break/>). Start tags and end tags surround content and possibly other markup, empty-element tags don’t surround anything.
- Unlike in HTML, you can choose the root element for your XML documents.
- An XML element’s start tag can contain one or more attributes.
### Character References and CDATA Sections
- Certain characters cannot appear literally in the content that appears between a start tag and an end tag or within an attribute value. For example, you cannot place a literal < character between a start tag and an end tag because doing so would confuse an XML parser into thinking that it had encountered another tag. 
- One solution to this problem is to replace the literal character with a character reference, which is a code that represents the character. Character references are classified as numeric character references or character entity references:
   - A numeric character reference refers to a character via its Unicode code point and adheres to the format &#nnnn; or &#xhhhh;, where nnnn provides a decimal representation of the code point and hhhh provides a hexadecimal representation.
   -  A character entity reference refers to a character via the name of an entity that specifies the desired character as its replacement text. Character entity references are predefined by XML and have the format &name;, in which name is the entity’s name. XML predefines five character entity references: &lt; ( <), &gt; ( >), &amp; ( &), &apos; ( '), and &quot; ( ").
-  A CDATA section is a section of literal HTML or XML markup and content surrounded by the <![CDATA[ prefix and the ]]> suffix. You don’t need to specify predefined character entity references within a CDATA section.
### Namespaces
- Namespacesare used to prevent name conflicts when elements and other XML language features appear.
- A namespace is a Uniform Resource Identifier (URI)-based container that helps differentiate XML vocabularies by providing a unique context for its contained identifiers. The namespace URI is associated with a namespace prefix by specifying, typically in an XML document’s root element, either the xmlns attribute by itself or the xmlns:prefix attribute, and assigning the URI to this attribute.
- A tag’s attributes don’t need to be prefixed when those attributes belong to the element. However, a prefix is required for attributes belonging to other namespaces.
### Comments and Processing Instructions 
- XML documents can contain comments, which are character sequences beginning with <!-- and ending with -->.
- XML also permits processing instructions to be present. A processing instruction is an instruction that’s made available to the application parsing the document.
## Well-Formed Documents
- XML is a much stricter language than HTML. To make XML documents easier to parse, XML mandates that XML documents follow certain rules:
   - All elements must either have start and end tags or consist of empty-element tags.
   - Tags must be nested correctly.
   - All attribute values must be quoted.
   - Empty elements must be properly formatted.
   - Be careful with case.
- XML parsersthat are aware of namespaces enforce two additional rules:
   - Each element and attribute name must not include more than one colon character.
   - No entity names, processing instruction targets, or notation names can contain colons.
- An XML document that conforms to these rules is well formed.
## Valid Documents
- A valid document adheres to constraints.
- Some XML parsers perform validation, whereas other parsers don’t. A parser that performs validation compares an XML document to a grammar document. Any deviation from the grammar documentis reported as an error to the application—the XML document isn’t valid. Validity errors aren’t necessarily fatal and the parser can continue to parse the XML document.
- Two commonly used grammar languages are Document Type Definition and XML Schema.
### Document Type Definition
- DTD grammar documents are written in accordance to a strict syntax that states what elements may be present and in what parts of a document, and also what is contained within elements and what attributes may be specified.
### XML Schema
- XML Schema is a grammar language for declaring the structure, content, and semantics (meaning) of an XML document.
