## 405: Not support GET/POST

- This is because we haven't extends HttpServlet or unable to @Override doGet/ doPost
- For the @Override, in Spring, at first, look at HttpServlet class and change the doGet HttpRquest and HttpResponse parameter's name to the same as HttpServlet class.
- Don't rename afterward. Even if it works right then. After u close Spring tool, it's not working

## Maven: r-click project doesn't have Deployment Discriptor in Java EE Tools
- Go to Help -> install -> Latest Eclipse realease -> Web/XML/JavaEE -> install them
- Maybe you need to install it 2 times

## Fixing Maven general error
- Run as -> Maven clean
- R-click on project -> Update Maven

## Fixed but server saved the cache
- R-click -> clean