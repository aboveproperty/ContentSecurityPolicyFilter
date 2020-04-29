Content Security Policy Filter (Java)
===========================

Adds the 'Content-Security-Policy' or 'Content-Security-Policy-Report-Only' Header to the response. 

Also see: 
 - http://content-security-policy.com/
 - http://www.w3.org/TR/CSP/#directives
 - https://developer.chrome.com/extensions/contentSecurityPolicy
 - https://developer.mozilla.org/en-US/docs/Web/Security/CSP

Normally you will only need a limited number or none of the init parameters. If no init parameter is defined the Header will look like this:

    Content-Security-Policy = default-src 'none'

Here is an example full configuration of the ContentSecurityPolicyFilter. 
 
        <filter>
           <filter-name>ContentSecurityPolicyFilter</filter-name>
           <filter-class>de.saville.csp.ContentSecurityPolicyFilter</filter-class>
           
           <init-param>
               <!-- If not specified the default is false -->
               <param-name>report-only</param-name>
               <param-value>false</param-value>
            </init-param>
            <!-- Optionally add a reporter-uri -->            
           <init-param>
               <param-name>report-uri</param-name>
               <param-value>/ContentSecurityPolicyReporter</param-value>
            </init-param>
           <init-param>
               <param-name>sandbox</param-name>
               <param-value>true</param-value>
               <!-- true enables the sandbox behaviour - the default is false - one can also specify exceptions, e.g.
               <param-value>allow-forms allow-same-origin</param-value>
               -->
            </init-param>
           <!-- Remember that special keywords have to be put in single quotes, e.g. 'none', 'self' -->
           <init-param>
               <!-- If not specified the default is 'none' -->
               <param-name>default-src</param-name>
               <param-value>'none'</param-value>
            </init-param>
           <init-param>
               <param-name>img-src</param-name>
                <param-value>http://*.example.com</param-value>
            </init-param>
           <init-param>
               <param-name>script-src</param-name>
               <param-value>'self' js.example.com</param-value>
            </init-param>
           <init-param>
               <param-name>style-src</param-name>
               <param-value>'self'</param-value>
            </init-param>  
           <init-param>
               <param-name>connect-src</param-name>
               <param-value>'self'</param-value>
            </init-param> 
           <init-param>
               <param-name>font-src</param-name>
               <param-value>'self'</param-value>
            </init-param>   
           <init-param>
               <param-name>object-src</param-name>
               <param-value>'self'</param-value>
            </init-param>  
           <init-param>
               <param-name>media-src</param-name>
               <param-value>'self'</param-value>
            </init-param> 
           <init-param>
               <param-name>frame-src</param-name>
               <param-value>'self'</param-value>
            </init-param>
            <init-param>
               <param-name>frame-ancestors</param-name>
               <param-value>'none'</param-value>
            </init-param>  
        </filter>
        
        <filter-mapping> 
           <filter-name>ContentSecurityPolicyFilter</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>
        
        
Optionally configure a Servlet to log the CSP violations:    
    
         <servlet>
             <servlet-name>ContentSecurityPolicyReporter</servlet-name>
             <servlet-class>de.saville.csp.ContentSecurityPolicyReporter</servlet-class>
         </servlet>
 
         <servlet-mapping>
             <servlet-name>ContentSecurityPolicyReporter</servlet-name>
             <url-pattern>/ContentSecurityPolicyReporter</url-pattern>
         </servlet-mapping>          
