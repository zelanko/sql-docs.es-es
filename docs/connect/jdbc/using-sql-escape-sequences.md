---
title: Usar secuencias de Escape SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: edf033fd91ecdd9ddd5ad33ce9a19e32f58b8bba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-sql-escape-sequences"></a>Usar secuencias de escape SQL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el uso de secuencias de escape SQL, tal como se define por la API de JDBC. Las secuencias de escape se usan dentro de una instrucción SQL para indicar al controlador que la parte de la secuencia de escape de la cadena SQL se debería tratar de forma diferente. Cuando el controlador JDBC procesa la parte de la secuencia de escape de una cadena SQL, traduce esa parte de la cadena en código SQL que SQL Server entiende.  
  
 Hay cinco tipos de secuencias de escape que la API JDBC requiere, y el controlador JDBC las admite todas:  
  
-   Literales comodín LIKE  
  
-   Tratamiento de funciones  
  
-   Literales de fecha y hora  
  
-   Llamadas a procedimientos almacenados  
  
-   Combinaciones externas  
  
-   Sintaxis de escape de LIMIT  
  
 La sintaxis de las secuencias de escape que usa el controlador JDBC es la siguiente:  
  
 `{keyword ...parameters...}`  
  
> [!NOTE]  
>  El proceso de escape SQL siempre está activado para el controlador JDBC.  
  
 En las secciones siguientes se describen los cinco tipos de secuencias de escape y cómo las admite el controlador JDBC.  
  
## <a name="like-wildcard-literals"></a>Literales comodín LIKE  
 El controlador JDBC admite el `{escape 'escape character'}` sintaxis para usar comodines de cláusulas LIKE como literales. Por ejemplo, el código siguiente devolverá valores para col3, donde el valor de col2 comienza literalmente con un guión (y no con su uso como comodín).  
  
```  
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```  
  
> [!NOTE]  
>  La secuencia de escape debe estar al final de la instrucción SQL. Para que haya varias instrucciones SQL en una cadena de comandos, la secuencia de escape tiene que estar al final de cada instrucción SQL pertinente.  
  
## <a name="function-handling"></a>Tratamiento de funciones  
 El controlador JDBC admite las secuencias de escape de funciones en instrucciones SQL con la sintaxis siguiente:  
  
```  
{fn functionName}  
```  
  
 donde `functionName` es una función compatible con el controlador JDBC. Por ejemplo:  
  
```  
SELECT {fn UCASE(Name)} FROM Employee  
```  
  
 En la tabla siguiente se muestran las diversas funciones que el controlador JDBC admite al usar un flujo de escape de funciones.  
  
|Funciones de cadena|Funciones numéricas|Funciones de fecha y hora|Funciones del sistema|  
|----------------------|-----------------------|------------------------|----------------------|  
|ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> ESPACIO<br /><br /> SUBSTRING<br /><br /> UCASE|ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE|CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> DAYOFWEEK<br /><br /> DAYOFYEAR<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> WEEK<br /><br /> YEAR|DATABASE<br /><br /> IFNULL<br /><br /> User|  
  
> [!NOTE]  
>  Si intenta utilizar una función que la base de datos no admita, se producirá un error.  
  
## <a name="date-and-time-literals"></a>Literales de hora y fecha  
 La sintaxis de las secuencias de escape para los literales de fecha, hora y marca de tiempo es la siguiente:  
  
```  
{literal-type 'value'}  
```  
  
 donde `literal-type` es uno de los siguientes:  
  
|Tipo de literal|Description|Formato de valor|  
|------------------|-----------------|------------------|  
|d|Date|aaaa-mm-dd|  
|t|Time|hh:mm:ss [1]|  
|ts|TimeStamp|aaaa-mm-dd hh:mm:ss[.f...]|  
  
 Por ejemplo:  
  
```  
UPDATE Orders SET OpenDate={d '2005-01-31'}   
WHERE OrderID=1025  
```  
  
## <a name="stored-procedure-calls"></a>Llamadas a procedimientos almacenados  
 El controlador JDBC admite el `{? = call proc_name(?,...)}` y `{call proc_name(?,...)}` sintaxis para llamadas a procedimientos almacenados, según si tiene que procesar un parámetro de valor devuelto de escape.  
  
 Un procedimiento almacenado es un objeto ejecutable almacenado en la base de datos. Normalmente, se trata de una o varias instrucciones SQL compiladas. La sintaxis de las secuencias de escape para llamar a un procedimiento almacenado es la siguiente:  
  
```  
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```  
  
 donde `procedure-name` especifica el nombre de un procedimiento almacenado y `parameter` especifica un parámetro de procedimiento almacenado.  
  
 Para obtener más información sobre el uso de la `call` secuencia con los procedimientos almacenados de escape, vea [instrucciones Using con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
## <a name="outer-joins"></a>Combinaciones externas  
 El controlador JDBC admite la sintaxis de combinación externa completa, derecha e izquierda de SQL92. La secuencia de escape para las combinaciones externas es:  
  
```  
{oj outer-join}  
```  
  
 donde outer-join es:  
  
```  
table-reference {LEFT | RIGHT | FULL} OUTER JOIN    
{table-reference | outer-join} ON search-condition  
```  
  
 donde `table-reference` es un nombre de tabla y `search-condition` es la condición de combinación que desea usar para las tablas.  
  
 Por ejemplo:  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status   
   FROM {oj Customers LEFT OUTER JOIN   
      Orders ON Customers.CustID=Orders.CustID}   
   WHERE Orders.Status='OPEN'  
```  
  
 El controlador JDBC admite las siguientes secuencias de escape de combinaciones externas:  
  
-   Combinaciones externas izquierdas  
  
-   Combinaciones externas derechas  
  
-   Combinaciones externas completas  
  
-   Combinaciones externas anidadas  
  
## <a name="limit-escape-syntax"></a>Sintaxis de Escape de limit  
  
> [!NOTE]  
>  La sintaxis de escape de LIMIT solo se admite con Microsoft JDBC Driver 4.2 (o superior) para SQL Server al usar JDBC 4.1 o posterior.  
  
 La sintaxis de escape de LIMIT se describe a continuación:  
  
```  
LIMIT <rows> [OFFSET <row offset>]  
```  
  
 La sintaxis de escape tiene dos partes: \< *filas*> es obligatorio y especifica el número de filas que se va a devolver. DESPLAZAMIENTO y \< *desplazamiento de fila*> son opcionales y especifique el número de filas que se omiten antes de empezar a devolver filas. El controlador JDBC solo admite el elemento obligatorio al transformar la consulta para que use TOP en lugar de LIMIT. SQL Server no admite la cláusula de LIMIT. **El controlador JDBC no admite el argumento opcional \<desplazamiento de fila > y el controlador, producirá una excepción si se utiliza**.  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
