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
Parsing XML is not a trivial task, but it is also not onerously difficult. The more you practice and familiarize yourself with XML in general, the faster your will become at parsing XML data.

XML tags can have data stored in the tags themselves, and identified as Elements, and they can have data stored in Attributes of the XML tags. There are [several sites that list XML tags](https://www.w3schools.com/xml/xml_elements.asp) and the accompanying rules for formatting them, as well as other ways that XML tags can be created and used. The reader is encouraged to at least skim these, because only a cursory explanation will be provided here that is directly relevant to parsing NCBI Pubmed data.

Continuing the example above, if we wanted to create an XML document that had valid syntax, it would start with a header that identified the version of XML and the document type to the software that read it. Next would come the \<html> tag, usually followed (but not required) by a comment line.  If we wanted to add an attribute to the \<div> tag, we could do that here as well. Single or double-quotes can be used in attributes, as well as nested single/double quotes.


        <?xml version="1.0" encoding="utf-8"?>
        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
        <html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
        <-- This is my first XML document -->
        <html>
          <h1>
            <div type="string">HelloWorld!</div>
          </h1>
        </html>
        


