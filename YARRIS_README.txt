Banyan raised 6 CVEs that exist for Struts 1.2.9 , documented in:
      https://www.cvedetails.com/vulnerability-list/vendor_id-45/product_id-6117/version_id-524237/Apache-Struts-1.2.9.html

- Most serious issue CVE-2014-0114 was already addressed by upgrading to commons-beanutils-1.9.4.jar many years ago in ConSol.
- This repo is a fork created from https://github.com/kawasima/struts1-forever.git:STRUTS_1_2_BRANCH , where this branch
STRUTS_1_2_BRANCH  already includes two fixes of the 6 issues: CVE-2016-1181 and CVE-2016-1182.
- In addition https://github.com/kawasima/struts1-forever.git:STRUTS_1_2_BRANCH also has an unaccepted Pull Request from
     pgbhagat fixing CVE-2015-0899 so the patch for this PR was pulled from github and applied here:

git apply pgbhagat_terasoluna_3fb0bf8e4b5d49e4611a2e1203c2ffd7418f8b41.patch.txt

    - more info : Looks like another patch from TERASOLUNA : https://osdn.net/projects/terasoluna/wiki/StrutsPatch2-EN => also found in PR
    - PR commit details => https://github.com/kawasima/struts1-forever/pull/1/commits/3fb0bf8e4b5d49e4611a2e1203c2ffd7418f8b41
    "Added a configuration item acceptPage in Struts configuration file(struts-config.xml).

    If acceptPage configuration is not done, irrespective of the value of "page" attribute, input check will be executed
    If acceptPage configuration is done, its value and value of "page" attribute is compared and the input check is performed based on the higher value. "

- remaining two issues are low severity:
    - CVE-2023-34396 (low)
    "When a Multipart request has non-file normal form fields, Struts used to bring them into memory as Strings without checking their sizes. This could lead to OOM if developer has set struts.multipart.maxSize to a value equal or greater than the available memory."
    - CVE-2023-34149 (low)
    https://cwiki.apache.org/confluence/display/WW/S2-063 : "WW-4620 added autoGrowCollectionLimit to XWorkListPropertyAccessor, but it only handles setProperty() and not getProperty(). This could lead to OOM if developer has set CreateIfNull to true for the underlying Collection type field."


problems found with this repo
-----------------------------

- Caused by: org.apache.jasper.JasperException: JBWEB004113: The absolute uri: http://jakarta.apache.org/struts/tags-bean cannot be resolved in either web.xml or the jar files deployed with this application
      => seems like base URI changed between v 1.0 (xdocs/userGuide/struts-bean.xml) "http://jakarta.apache.org/struts/tags-bean" and
          v 1.2 (doc/userGuide/struts-bean.xml) "http://struts.apache.org/tags-bean", therefore updating refs in ConSol
          ajaxTagLibs.jsp , taglibDirectives.inc , taglibs.jsp
