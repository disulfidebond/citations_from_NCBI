## Overview
This writeup describes the basics of XML, as well as a few tips on deciphering XML from websites.

### What XML is
[XML](https://www.w3schools.com/xml/xml_whatis.asp) is short for eXtensible Markup Language, and has a variety of uses, from programming to web design. 

Contrary to what you might expect, XML does not directly perform actions. If you were to write the obligatory 'Hello World' in XML, it would be something like:

        <html>
          <h1>
            <div>HelloWorld!</div>
          </h1>
        </html>

XML uses tags, such as \<html> , to hold data or information.  A more concrete and familiar example is the xml for a webpage. Each tag holds information that the browser uses to instruct it how to display the webpage. 

To recap:
* There are no binaries that 'run' XML; you cannot open a Bash window and type _xml hello world_
* XML is comprised of tags that contain information, and **every** tag must have a closing tag. In the above example, the \<html> opening tag and the \<div> opening tag are closed by \</html> and \</div> respectively.
* The formatting of XML can vary widely, and with few exceptions, as long as the above criteria of an open tag and a close tag are followed, syntactically the XML document is correct.  This XML snippet is completely identical to the example above, but is much less readable:

        <html><h1><div>HelloWorld!</div></h1></html>
        
### More XML
XML is a very structured language, which makes it ideal for holding data.  In the example above, the \<html> tag is the root tag, \<h1> is a child tag of \<html>, and \<div> is a child tag of \<h1>

XML can have data stored in the tags themselves, and are identified for parsing purposes as Elements. They can also have data stored in Attributes of the XML tags. There are [several sites that list XML tags](https://www.w3schools.com/xml/xml_elements.asp) and the accompanying rules for formatting them, as well as other ways that XML tags can be created and used. The reader is encouraged to at least skim these, because only a cursory explanation will be provided here that is directly relevant to parsing NCBI Pubmed data.

Continuing the example above, if we wanted to create an XML document that had valid syntax, it would start with a header that identified the version of XML and the document type to the software that read it. Next would come the \<html> tag, usually followed (but not required) by a comment line.  If we wanted to add an attribute to the \<div> tag, we could do that here as well. Single or double-quotes can be used in attributes, as well as nested single/double quotes.


        <?xml version="1.0" encoding="utf-8"?>
        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
        <html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
        <-- This is my first XML document -->
          <h1>
            <div type="string">HelloWorld!</div>
          </h1>
        </html>
        
### Parsing XML
Parsing XML is not a trivial task, but it is also not onerously difficult. The more you practice and familiarize yourself with XML in general, the faster your will become at parsing XML data.

A typical problem with parsing is simply being able to decipher the data, particularly if the XML document is simply pulled (or 'scraped') from a website. There are numerous tools that make reading XML easier; one example is TextEdit on MacOSX will automatically render an XML document into something similar to what a webpage would show unless you explicitly tell it not to do so.

When parsing XML, one might be tempted to use grep or regular expressions (Regex), however, this should only be done as a last resort, for several reasons, including:
* As mentioned above, XML can have numerous tags on a single line, and most flavors of Regex rely on scanning multiple lines.
* You will have to create absurdly long Regex patterns just to separate XML tags
* Typically you need to at least have an idea of what keyword or anchor that you are looking for before starting, which can be a nontrivial task in itself

One example shown here to at least partly sort an XML file can be used with the [Atom](https://atom.io) text editor:

* Create a new blank Atom document, then copy and paste the XML into that document.  Next, do a search/replace for '><' , to be replaced by '>' followed by a newline, followed by '<' 
  * (Important: you will have to copy a newline from a text document, or use the "Regex" option with '\n'.  The code below can be copied and pasted into the Replace field)

        >
        
        <

![](https://github.com/disulfidebond/citations_from_NCBI/blob/master/parsingTrick1_ATOM.png)

* Click 'Replace All'
![](https://github.com/disulfidebond/citations_from_NCBI/blob/master/parsingTrick2_ATOM.png)

**Ta-Daaa!**

From here, it is much easier to identify the tags containing the data that you'd like to parse.  For example, if you wanted to extract the title, the pseudocode for this would be:

        xml_tree = dataFromXMLDocument
        for tag in xml_tree:
          if tag_identifier is 'h1':
            print tag_identifier
            # will print 'Major histocompatibility complex haplotyping and long-amplicon allele discovery in cynomolgus macaques...'
            
A parser for PubMed has been created in this repo, and [is available here]().
