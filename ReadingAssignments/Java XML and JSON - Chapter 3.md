# CHAPTER 3
## What is DOM?
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
## Obtain a DOM Parser/DocumentBuilder
- Obtain a DOM parser/document builder by first instantiating DocumentBuilderFactory, by calling one of its newInstance() class methods:
                  DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
- Behind the scenesm newInstance() follows an ordered lookup procedure to identify the DocumentBuilderFactory implementation class to load.
  - The procedure first examnines the javax.xml.persers.DocumentBuilderFactory system property
  - And chooses the Java platform's default DocumentBuilderFactory implementation class when no other class is found.
- If an implementation class isnt available or cant be instantiated, newInstance() throws an instance of the FactoryConfigurationError class.
- Otherwise, it instantitiates the class and returns its instance.
- After obtaining a DocumentBuilderFactory instance, you can call various configuration methods to configure the factory.
- -After the factory has been configured, call its DocumentBuilder newDocumentBuilder() method to return a document builder that supports the configuration
                  DocumentBuilder db = dbf.newDocumentBuilder();
- If a document builder cannot be returned, this method throws a ParserConfigurationException instance.
## Parsing and Creating XML Documents
- Node declares severalmethods for navigating the node tree
  - boolean hasChildNodes(): returns true when a node as child nodes.
  - Node getFirstChild(): returns the node's first chhild.
  - Node getLastChild(): returns the node's last child.
- Nodes declares 4 methods for modifying the tree
  - Node insertBefore(Node newChild, Node refChild): inserts newChild before the existing node specified by refChild and returns newChild.
  - Node removeChild(Node oldChild): removes the child node identified by oldChild from the tree and returns oldChild.
  - Node replaceChild (Node newChild, Node oldChild): replaces oldChild with newChild and returns oldChild.
  - Node appendChild (Node newChild): adds newChild to the end of the current node’s child nodes and returns newChild.
- Also node declares several utility methods: 
  - cloneNode(boolean deep): create and return a duplicate of the current node, recursively cloning its subtree when true is passed to deep.
  - void normalize(): descend the tree from the given node and merge all adjacent text nodes, deleting those text nodes that are empty.
- Document declares three methods for locating one or more elements :
  - Element getElementById(String elementId): returns the element that has an id attribute matching the value specified by elementId. 
  - NodeList getElementsByTagName(String tagname): returns a nodelist of a document’s elements (in document order) matching the specified tagName.
  
  

