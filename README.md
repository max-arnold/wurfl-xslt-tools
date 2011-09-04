WURFL XSLT Tools
================
by Roland Guelle <roldriguez@users.sourceforge.net>, http://guelle.de


The WURFL information is stored in XML. So the simpliest way to manipulate and transform WURFL is XSLT.

These stylesheets are tested with xsltproc from the package libxslt (http://xmlsoft.org/XSLT). I only use this on the command line, if you need a GUI - there are lot of tools that helps you working with XSLT. Some exslt extensions are used, so please check if your XSLT processor supports this.

If you have never worked with a XSLT processor or the command line before, add to WURFL and open the file with Firefox.


## check_wurfl.xsl
Check your patched/modified WURFL consistency:

* id attribute is present and unique
* user_agent attribute is present and unique
* fall_back is available and could be resolved

    xsltproc check_wurfl.xsl wurfl.xml
	
	
## convert\_2\_html.xsl
Create a simple WURFL.xml HTML page

    xsltproc convert_2_html.xsl wurfl.xml > wurfl.html

## convert\_wurfl\_markups.xsl
Convert the WURFL markups to ''outdated'' names. Some years ago the markup names have changed from wml11 to wml_1_1.

    xsltproc convert_wurfl_markups.xsl wurfl.xml > wurfl_converted.xml

## count\_useragents.xsl
Answer the question "how many useragents/capabilities are stored in WURFL?"

    xsltproc count_useragents.xsl wurfl.xml

## get\_capabilities.xsl
Get capabilities (without groups) from WURFL.

    xsltproc --stringparam 'ua' "Nokia3650" get_capabilities.xsl wurfl.xml
    xsltproc --stringparam 'id' "nokia_3650_ver1" get_capabilities.xsl wurfl.xml

## patch_wurfl.xsl
Patch WURFL with your own devices, groups and capabilities.

    xsltproc --stringparam 'file' "your_patch_file" patch_wurfl.xsl wurfl.xml > wurfl_patched.xml

## remove\_elements.xsl / remove\_elements.xml
WURFL has many capabilities and groups. If you don't need all capabilities, you could remove them.

    xsltproc --stringparam 'file' "remove_elements.xml" remove_elements.xsl wurfl.xml > my_wurfl.xml

remove_elements.xml:

    <?xml version="1.0" encoding="utf-8"?>
    <elements>
      !--
      configuration file for remove_elements.xsl,
      send comments, questions to roland guelle <roldriguez@users.sourceforge.net>
      -->
      <groups>
        <group>wta</group>
        <group>object_download</group>
        <group>streaming</group>
        <group>wap_push</group>
        <group>j2me</group>
        <group>mms</group>
        <group>sms</group>
        <group>sound_format</group>
      </groups>
      <capabilities>
        <capability>tiff</capability>
        <capability>bmp</capability>
      </capabilities>
    </elements>

## roll\_out\_into\_sql.xsl / roll\_out\_capabilities.xml
Resolve WURFL fallbacks for all values and capabilities defined in roll_out_capabilities.xml and create SQL statements for insert WURFL into a SQL database.

    xsltproc roll_out_into_sql.xsl wurfl.xml > wurfl.sql

## roll\_out\_into\_txt.xsl / roll\_out\_capabilities.xml
Resolve WURFL fallbacks for all values and capabilities defined in roll_out_capabilities.xml and create text/csv output.

    xsltproc roll_out_into_txt.xsl wurfl.xml > wurfl.txt

## roll\_out\_into\_xml.xsl / roll\_out\_capabilities.xml
Resolve WURFL fallbacks for all values and capabilities defined in roll_out_capabilities.xml and create XML output.

    xsltproc roll_out_into_xml.xsl wurfl.xml > wurfl_resolved.xml

## tidy_config
Useful tidy (http://tidy.sourceforge.net/tidy) configuration.
