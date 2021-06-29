#CHAPTER 3
##What is DOM?
- Document Object Model (DOM) is a Java API for parsing an XML document into an in-memory tree of nodes, and for creating an XML document from a node tree. Adter a DOM parser creates a tree, an application uses the DOM API to navigate over and extract infoset item from the tree's nodes.
- The size of documents parsed or created by DOM is limited by the amount of available memory for storing the documents's node-based tree structure.
## A tree of nodes
- DOM views an XML document as a tree that is composed of several kinds of nodes.
- Each node has a node name, which is the complete name for nodes that have names, and #node-type for unnamed nodes, where node-type is one of data-section, comment, document, document-fragment or text. NOdes also have local names (names without prefixes), prefixed, and namespace URIs. 
- Nodes have string values, which happen to be the content of text nodes, comment nodes, and similar text-oriented nodes, normlaiezed values for attributes , and null for everything else.
- DOM classifies nodes into 12 types, of which seven types can be considered part of a DOM tree:
  - Attribute node
  - CDATA section node
  - Comment node
  - Document node
  - Document fragment node
  - Document type node
  - Element node
  - Entity node
  - Entity node
  - Entity reference node
  - Processing instruction node
  - Text node
- Although these node types store considerable information about an XML document, there are limitations.
- DOM Level 3 addresses some of the DOM's various limitations.
- A DOM parser is also known as a document builder because of its dual role in parsing and creating XML documents.
- Obtain a DOM parser/document builder by first instantiating DocumentBuilderFactory, by calling one of its newInstance() class methods:
                  DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
  
  

