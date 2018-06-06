---
title: Compatibilidad con la intercalación y Unicode | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: collations
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 25b36b25efbb7c99d3595da26587007f784bfc25
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708043"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporcionan propiedades de distinción entre mayúsculas y minúsculas, acentos y reglas de ordenación para los datos. Las intercalaciones que se usan con tipos de datos de caracteres como **char** y **varchar** dictan la página de códigos y los caracteres correspondientes que se pueden representar para ese tipo de datos. Si va a instalar una instancia nueva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], restaurar una copia de seguridad de la base de datos o conectar el servidor a bases de datos cliente, es importante conocer los requisitos de configuración regional, el criterio de ordenación y la distinción entre mayúsculas y minúsculas y acentos de los datos con los que está trabajando. Para ver una lista de las intercalaciones disponibles en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md).    
    
 Al seleccionar una intercalación para un servidor, base de datos, columna o expresión, se están asignando ciertas características a los datos que afectan a los resultados de muchas operaciones de la base de datos. Por ejemplo, cuando se crea una consulta con ORDER BY, el criterio de ordenación del conjunto de resultados puede depender de la intercalación que se aplica a la base de datos o que se dicta en una cláusula COLLATE en el nivel de expresión de la consulta.    
    
 Para hacer el mejor uso posible de la compatibilidad con la intercalación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se deben conocer los términos que se definen en este tema y cómo se relacionan con las características de los datos.    
    
##  <a name="Terms"></a> Términos de intercalación    
    
-   [Intercalación](#Collation_Defn)    
    
-   [Configuración regional](#Locale_Defn)    
    
-   [Página de códigos](#Code_Page_Defn)    
    
-   [Criterio de ordenación](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> Intercalación    
 Una intercalación especifica los patrones de bits que representan a cada carácter de un conjunto de datos. Las intercalaciones también determinan las reglas que ordenan y comparan los datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite almacenar los objetos que tienen intercalaciones diferentes en una sola base de datos. En las columnas que no sean Unicode, la configuración de intercalación especifica la página de códigos de los datos y qué caracteres se pueden representar. Los datos que se mueven entre columnas que no sean Unicode se deben convertir de la página de códigos de origen a la página de códigos de destino.    
    
 Los resultados de las instrucciones de[!INCLUDE[tsql](../../includes/tsql-md.md)] pueden variar cuando se ejecutan en el contexto de bases de datos distintas que tengan una configuración de intercalación diferente. Si es posible, utilice una intercalación normalizada para su organización. De esta manera no tiene que especificar explícitamente la intercalación en cada carácter o expresión Unicode. Si debe trabajar con objetos que tienen configuraciones de intercalación y de página de códigos diferentes, conviene codificar las consultas para tener en cuenta las reglas de prioridad de intercalación. Para obtener más información, vea [Prioridad de intercalación (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md).    
    
 Las opciones asociadas con una intercalación son la distinción de mayúsculas y minúsculas, la distinción de acentos, la distinción de tipos de kana, la distinción de ancho y la distinción de selector de variación. Estas opciones se especifican anexándolas al nombre de intercalación. Por ejemplo, la intercalación `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` es una intercalación con distinción de mayúsculas y minúsculas, distinción de acentos, distinción de tipos de kana y distinción de ancho. Otro ejemplo: la intercalación `Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS` distingue mayúsculas y minúsculas, los acentos, los tipos de kana, el ancho y el selector de variación.  En la tabla siguiente se describe el comportamiento asociado a estas diversas opciones.    
    
|Opción|Descripción|    
|------------|-----------------|    
|Distinguir mayúsculas de minúsculas (_CS)|Distingue entre letras mayúsculas y minúsculas. Si se selecciona, las letras minúsculas se ordenan por delante de sus versiones en mayúsculas. Si esta opción no está seleccionada, la intercalación no distinguirá mayúsculas de minúsculas. Es decir, que SQL Server considera las versiones mayúscula y minúscula de las letras como letras idénticas para fines de ordenación. Puede seleccionar explícitamente no distinguir entre mayúsculas y minúsculas especificando _CI.|    
|Distinguir acentos (_AS)|Distingue entre caracteres acentuados y no acentuados. Por ejemplo, 'a' no es igual a 'ấ'. Si esta opción no está seleccionada, la intercalación no distinguirá acentos. Es decir, que SQL Server considera las versiones acentuadas y no acentuadas de las letras como letras idénticas para fines de ordenación. Puede seleccionar explícitamente no distinguir acentos especificando _AI.|    
|Distinguir kana (_KS)|Distingue entre los dos tipos de caracteres Kana japoneses: Hiragana y Katakana. Si esta opción no está seleccionada, la intercalación no distinguirá los caracteres kana. Es decir, que SQL Server considera los caracteres Hiragana y Katakana como caracteres iguales para la ordenación. La omisión de esta opción es el único método para especificar Kana-insensibilidad.|    
|Distinguir ancho (_WS)|Distingue entre caracteres de ancho total y ancho medio. Si no se activa esta opción, SQL Server considera que la representación de ancho completo y de ancho medio del mismo carácter son idénticas para la ordenación. La omisión de esta opción es el único método para especificar no distinción de ancho.|    
|Distinguir selector de variación (_VSS) | Distingue distintos selectores de variación ideográfica en las intercalaciones del japonés Japanese_Bushu_Kakusu_140 y Japanese_XJIS_140, introducidas por primera vez en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. Una secuencia de variación consta de un carácter base y de un selector de variación adicional. Si no se selecciona la opción _VSS, la intercalación no distinguirá el selector de variación y este no se tendrá en cuenta en la comparación. Es decir, SQL Server considera que los caracteres que se basan en el mismo carácter base con diferentes selectores de variación son idénticos con fines de ordenación. Consulte también  [Unicode Ideographic Variation Database](http://www.unicode.org/reports/tr37/)(Base de datos de variaciones ideográficas de Unicode). <br/><br/> Las intercalaciones que distinguen selectores de variación (_VSS) no se admiten en los índices de búsqueda de texto completo. Los índices de búsqueda de texto completo solo admiten opciones que distinguen acentos (_AS), que distinguen kana (_KS) y que distinguen ancho (_WS). Los motores XML y CLR de SQL Server no admiten selectores de variación (_VSS).
    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite los siguientes conjuntos de intercalación:    
    
 intercalaciones de Windows    
 Las intercalaciones de Windows definen reglas para almacenar los datos de caracteres que se basan en una configuración regional del sistema Windows asociada. En una intercalación de Windows, la comparación de datos no Unicode se implementa con el mismo algoritmo que la de los datos Unicode. Las reglas de intercalación básicas de Windows especifican qué alfabeto o idioma se utilizan cuando se aplica un orden de diccionario, y la página de códigos que se usa para almacenar los datos de caracteres que no son Unicode. Tanto la ordenación Unicode y como la ordenación no Unicode son compatibles con comparaciones de cadenas de una determinada versión de Windows. De este modo se proporciona coherencia entre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y también se ofrece a los programadores la posibilidad de ordenar las cadenas de sus aplicaciones usando las mismas reglas que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md).    
    
 Intercalaciones binarias    
 Las intercalaciones binarias ordenan los datos según la secuencia de valores codificados definidos por la configuración regional y el tipo de datos. Distinguen entre mayúsculas y minúsculas. Una intercalación binaria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define la configuración regional y la página de códigos ANSI que se usa. Esto exige un criterio de ordenación binario. Dado que son relativamente simples, las intercalaciones binarias ayudan a mejorar el rendimiento de la aplicación. En los tipos de datos no Unicode, las comparaciones de datos se basan en los puntos de código que se definen en la página de códigos ANSI. En tipos de datos Unicode, las comparaciones de datos dependen de los puntos de código Unicode. En intercalaciones binarias de tipos de datos Unicode, la configuración regional no se tiene en cuenta a la hora de ordenar los datos. Por ejemplo, Latin_1_General_BIN y Japanese_BIN producen resultados de orden idénticos cuando se usan en datos Unicode.    
    
 Hay dos tipos de intercalaciones binarias en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; las intercalaciones **BIN** antiguas y las intercalaciones **BIN2** nuevas. En una intercalación **BIN2** todos los caracteres se ordenan de acuerdo a sus puntos de código. En una intercalación **BIN** solamente el primer carácter se ordena de acuerdo al punto de código y el resto de ellos se ordenan según sus valores de byte. (Dado que la plataforma de Intel tiene una arquitectura "litte endian", los caracteres de codificación Unicode siempre se intercambian por bytes).    
    
 Intercalaciones de SQL Server    
 Las intercalaciones de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_*) son compatibles en cuanto al criterio de ordenación con las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las reglas de ordenación alfabética de datos no Unicode son incompatibles con cualquier rutina de ordenación suministrada por los sistemas operativos Windows. Sin embargo, la ordenación de datos Unicode es compatible con una versión especial de las reglas de ordenación de Windows. Como las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usan reglas de comparación diferentes para los datos Unicode y para los que no son Unicode, ve resultados diferentes en las comparaciones de los mismos datos, dependiendo del tipo de datos subyacente. Para obtener más información, vea [Nombre de intercalación de SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).    
    
> [!NOTE]    
>  Al actualizar una instancia en idioma inglés de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se puede especificar la compatibilidad de las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_*) con las instancias existentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como la intercalación predeterminada de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se define durante la instalación, asegúrese de especificar con cuidado la configuración de la intercalación cuando se cumple lo siguiente:    
>     
>  -   El código de la aplicación depende del comportamiento de las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores.    
> -   Se deben almacenar datos de caracteres que reflejen varios idiomas.    
    
 Se admite el establecimiento de intercalaciones en los siguientes niveles de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:    
    
 Intercalaciones de nivel de servidor    
 La intercalación predeterminada de servidor se establece durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y también se convierte en la intercalación predeterminada de las bases de datos del sistema y de todas las bases de datos del usuario. Observe que las intercalaciones exclusivas de Unicode no pueden seleccionarse durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque no se admiten como intercalaciones de nivel de servidor.    
    
 Después de que una intercalación se haya asignado al servidor, no puede cambiar la intercalación excepto exportando todos los objetos y datos de base de datos, recompilando la base de datos **master** e importando todos los objetos y datos de base de datos. En lugar de cambiar la intercalación predeterminada de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar la intercalación deseada en el momento de crear una base de datos o una columna de base de datos.    
    
 Intercalaciones de nivel de base de datos    
 Cuando se crea una base de datos, se puede usar la cláusula COLLATE de la instrucción CREATE DATABASE para especificar la intercalación predeterminada de la base de datos. Si no se especifica ninguna intercalación, se asigna a la base de datos la intercalación de servidor.    
    
 No puede cambiar la intercalación de base de datos del sistema excepto cambiando la intercalación del servidor.    
    
 La intercalación de base de datos se usa para todos los metadatos de la base de datos, y es la predeterminada para todas las columnas de cadena, los objetos temporales, los nombres de variable, y cualquier otra cadena usada en la base de datos. Cuando se cambia la intercalación de una base de datos de usuario, pueden producirse conflictos de intercalación cuando las consultas en la base de datos tienen acceso a tablas temporales. Las tablas temporales se almacenan siempre en la base de datos del sistema de **tempdb**, que usa la intercalación de la instancia. Las consultas que comparan datos de caracteres entre la base de datos de usuario y **tempdb** pueden generar un error si las intercalaciones producen un conflicto en la evaluación de los datos de caracteres. Puede resolver esto especificando la cláusula COLLATE en la consulta. Para obtener más información, vea [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).    
    
 Intercalaciones de columna    
 Cuando cree o altere una tabla, puede especificar intercalaciones para cada columna de cadena de caracteres mediante la cláusula COLLATE. Si no se especifica una intercalación, a la columna se le asigna la intercalación predeterminada de la base de datos.    
    
 Intercalaciones de nivel de expresión    
 Las intercalaciones de nivel de expresión se establecen cuando se ejecuta una instrucción y afectan al modo en que se devuelve un conjunto de resultados. Esto permite que los resultados de la ordenación ORDER BY sean específicos de la configuración regional. Utilice una cláusula COLLATE como la siguiente para implementar intercalaciones de nivel de expresión:    
    
```    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> Configuración regional    
 Una configuración regional es un conjunto de información que está asociado a una ubicación o cultura. Puede incluir el nombre e identificador del idioma hablado, la escritura que se usa para escribir el idioma y las convenciones culturales. Las intercalaciones pueden estar asociadas a una o varias configuraciones regionales. Para obtener más información, vea [Id. de configuración regional asignados por Microsoft](http://msdn.microsoft.com/goglobal/bb964664.aspx).    
    
###  <a name="Code_Page_Defn"></a> Code Page    
 Una página de códigos es un juego ordenado de caracteres en un script determinado en el que un índice numérico, o un valor de punto de código, está asociado con cada carácter. Una página de códigos de Windows se denomina normalmente *juego de caracteres* o *charset*. Las páginas de códigos se usan para ofrecer compatibilidad con los juegos de caracteres y las distribuciones de teclado que se usan en distintas configuraciones regionales del sistema Windows.     
###  <a name="Sort_Order_Defn"></a> Sort Order    
 El criterio de ordenación especifica cómo se ordenan los valores de datos. Esto afecta a los resultados de la comparación de los datos. Los datos se ordenan con las intercalaciones, y se pueden optimizar mediante los índices.    
    
##  <a name="Unicode_Defn"></a> Compatibilidad con Unicode    
 Unicode es un estándar que permite asignar puntos de código con caracteres. Puesto que se ha diseñado para cubrir todos los caracteres de todos los idiomas del mundo, no es preciso usar páginas de códigos diferentes para controlar los distintos juegos de caracteres. Si almacena datos de caracteres que reflejan varios idiomas, use siempre tipos de datos Unicode (**nchar**, **nvarchar**y **ntext**) en lugar de tipos de datos que no sean Unicode (**char**, **varchar**y **text**).    
    
 Hay limitaciones significativas asociadas a los tipos de datos no Unicode. Esto se debe a que un equipo no Unicode se limita a usar una única página de códigos. Podría experimentar una ganancia en el rendimiento mediante Unicode porque se requieren menos conversiones de páginas de códigos. Las intercalaciones Unicode deben seleccionarse de forma individual en el nivel de expresión, base de datos o columna porque no se admiten en el nivel de servidor.    
    
 Las páginas de códigos que un cliente usa se determinan en la configuración del sistema operativo. Para establecer las páginas de códigos del cliente en los sistemas operativos Windows, use **Configuración regional** en el Panel de control.    
    
 Al mover los datos de un servidor a un cliente, los controladores de cliente anteriores podrían no reconocer la intercalación del servidor. Esto puede ocurrir al mover los datos de un servidor Unicode a un cliente no Unicode. La mejor opción podría ser actualizar el sistema operativo cliente para que las intercalaciones del sistema subyacentes se actualicen. Si el cliente tiene instalado software cliente de base de datos, se puede considerar la posibilidad de aplicar a dicho software una actualización de servicio.    
    
 También puede intentar utilizar una intercalación diferente para los datos del servidor. Elija una intercalación que se asigne a una página de códigos en el cliente.    
    
 Para usar las intercalaciones UTF-16 disponibles en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a fin de mejorar la búsqueda y la ordenación de algunos caracteres Unicode (solo intercalaciones de Windows), puede seleccionar una de las intercalaciones de caracteres adicionales (_SC) o una de las intercalaciones de la versión 140.    
    
 Para evaluar completamente los problemas relacionados con el uso de tipos de datos Unicode y no Unicode, pruebe su escenario para cuantificar las diferencias de rendimiento en su entorno. Se recomienda normalizar la intercalación que se usa en los sistemas de una organización e implementar servidores y clientes Unicode siempre que sea posible.    
    
 En muchos casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interactúa con otros servidores o clientes, y la organización podría usar varios estándares de acceso a datos entre las aplicaciones y las instancias de servidor. Los clientes[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son uno de los dos tipos principales:    
    
-   **Clientes Unicode** que usan OLE DB y Conectividad abierta de bases de datos (ODBC) versión 3.7 o posteriores.    
    
-   **Clientes no Unicode** que usan DB-Library y ODBC versión 3.6 o anteriores.    
    
 En la tabla siguiente se proporciona información acerca de cómo usar datos multilingües con varias combinaciones de servidores Unicode y no Unicode.    
    
|Servidor|Cliente|Beneficios o limitaciones|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|Dado que los datos Unicode se usan en todo el sistema, este escenario proporciona el máximo rendimiento y protección frente a daños de los datos recuperados. Se trata de la situación de Objetos de datos ActiveX (ADO), OLE DB y ODBC versión 3.7 o posteriores.|    
|Unicode|No Unicode|En este escenario y especialmente con las conexiones entre un servidor que ejecuta un sistema operativo más reciente y un cliente que ejecuta una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o un sistema operativo anterior, puede haber limitaciones o producirse errores al mover los datos a un equipo cliente. Los datos Unicode del servidor intentan asignarse a una página de códigos correspondiente en el cliente no Unicode para convertir los datos.|    
|No Unicode|Unicode|No es una configuración ideal para utilizar datos multilingües. No puede escribir los datos Unicode en el servidor no Unicode. Es probable que se produzcan problemas si los datos se envían a servidores externos a la página de códigos del servidor.|    
|No Unicode|No Unicode|Se trata de un escenario muy limitado para datos multilingües. Puede usar solo una única página de códigos.|    
    
##  <a name="Supplementary_Characters"></a> Caracteres complementarios    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona tipos de datos, como **nchar** y **nvarchar** , para almacenar los datos Unicode. Estos tipos de datos codifican el texto en un formato denominado *UTF-16*. Unicode Consortium asigna a cada carácter un punto de código único, que es un valor en el intervalo comprendido entre 0x0000 y 0x10FFFF. Los caracteres que se usan con más frecuencia tienen valores de punto de código que se ajustan a una palabra de 16 bits en memoria y en disco, pero los caracteres con valores de punto de código mayores que 0xFFFF requieren dos palabras de 16 bits consecutivas. Estos caracteres se denominan *caracteres adicionales*y las dos palabras de 16 bits consecutivas, *pares suplentes*.    
    
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], se puede usar una nueva familia de intercalaciones de caracteres adicionales (_SC) con los tipos de datos **nchar**, **nvarchar** y **sql_variant**. Por ejemplo: `Latin1_General_100_CI_AS_SC`o `Japanese_Bushu_Kakusu_100_CI_AS_SC`si usa una intercalación japonesa.    

 A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], todas las nuevas intercalaciones admiten automáticamente los caracteres adicionales.

 Si utiliza caracteres adicionales:    
    
-   Los caracteres adicionales se pueden utilizar en las operaciones de ordenación y comparación en las versiones de intercalación 90 o mayores.    
    
-   Todas las intercalaciones de la versión 100 admiten la ordenación lingüística con caracteres adicionales.    
    
-   Los caracteres adicionales no son compatibles con metadatos, como nombres de objetos de base de datos.    
    
-   Las bases de datos que usan intercalaciones con caracteres adicionales (\_SC), no se pueden habilitar para la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto se debe a que algunas de las tablas del sistema y los procedimientos almacenados que se crean para la replicación usan el tipo de datos **ntext** heredado, que no admite caracteres adicionales.  
    
-   La marca SC se puede aplicar a:    
    
    -   Intercalaciones de la versión 90    
    
    -   Intercalaciones de la versión 100    
    
-   La marca SC no se puede aplicar a:    
    
    -   Intercalaciones de Windows sin versión de la versión 80    
    
    -   Intercalaciones binarias BIN o BIN2    
    
    -   Intercalaciones SQL\*    
    
    -   Intercalaciones de la versión 140 (estas no necesitan la marca SC, dado que ya admiten caracteres adicionales)    
    
 En la siguiente tabla se compara el comportamiento de algunas funciones de cadena y algunos operadores de cadena cuando usan caracteres adicionales con y sin intercalación de caracteres adicionales (SCA):    
    
|Función u operador de cadena|Con intercalación de caracteres adicionales (SCA)|Sin intercalación SCA|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|El par suplente de UTF-16 se cuenta como un solo punto de código.|El par suplente de UTF-16 se cuenta como dos puntos de código.|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|Estas funciones tratan los pares suplentes como un solo punto de código y funcionan de la forma esperada.|Estas funciones pueden dividir cualquier par suplente y provocar resultados inesperados.|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|Devuelve el carácter correspondiente al valor del punto de código Unicode especificado en el intervalo comprendido entre 0 y 0x10FFFF. Si el valor especificado está en el intervalo comprendido entre 0 y 0xFFFF, solo se devuelve un carácter. Con valores más altos, se devuelve el suplente correspondiente.|Un valor mayor que 0xFFFF devuelve NULL en vez del suplente correspondiente.|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|Devuelve un punto de código UTF-16 en el intervalo comprendido entre 0 y 0x10FFFF.|Devuelve un punto de código UCS-2 en el intervalo comprendido entre 0 y 0xFFFF.|    
|[Hacer coincidir un carácter comodín](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [Carácter comodín - caracteres no coincidentes](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|Se admiten caracteres adicionales para todas las operaciones de caracteres comodín.|No se admiten caracteres adicionales para estas operaciones de caracteres comodín. Se admiten otros operadores de caracteres comodín.|    
    
##  <a name="GB18030"></a> Compatibilidad con GB18030    
 GB18030 es un estándar independiente que se usa en la República Popular China para codificar caracteres chinos. En GB18030, los caracteres pueden tener una longitud de 1, 2 o 4 bytes. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite caracteres de codificación GB18030, reconociéndolos en el momento de su entrada en un servidor procedentes de una aplicación del lado cliente y convirtiéndolos y almacenándolos de forma nativa como caracteres Unicode. Una vez almacenados en el servidor, se tratan como caracteres Unicode en las operaciones siguientes. Puede usar cualquier intercalación china, preferentemente la más reciente: la versión 100. Todas las intercalaciones de nivel _100 admiten la ordenación lingüística con caracteres GB18030. Si los datos incluyen caracteres suplementarios (pares suplentes), puede usar las intercalaciones SC disponibles en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para mejorar la búsqueda y la clasificación.    
    
##  <a name="Complex_script"></a> Compatibilidad con escritura compleja    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede admitir la entrada, el almacenamiento, el cambio, y la visualización de escrituras complejas. Entre los ejemplos de escritura compleja se encuentran los siguientes tipos:    
    
-   Escritura que incluye la combinación de texto de derecha a izquierda y de izquierda a derecha, caso de una combinación de textos en árabe e inglés.    
-   Escritura cuyos caracteres cambian de forma dependiendo de su posición, o al combinarse con otros caracteres como, por ejemplo, los caracteres del árabe, el índico y el tailandés.    
-   Idiomas como el tailandés que necesitan diccionarios internos para reconocer palabras porque no existen cortes entre ellas.    
    
Las aplicaciones de base de datos que interactúan con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben utilizar controles que sean compatibles con escritura compleja. Los controles de formato estándar de Windows creados en código administrado están habilitados para escritura compleja.    

##  <a name="Japanese_Collations"></a> Intercalaciones japonesas agregadas en  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]
 
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], se admiten dos nuevas familias de intercalaciones japonesas, con las permutaciones de varias opciones (\_CS, \_AS, \_KS, \_WS, \_VSS). 

Para obtener una lista de estas intercalaciones, puede consultar al Motor de base de datos de SQL Server:
``` 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

Todas las nuevas intercalaciones tienen compatibilidad integrada con los caracteres adicionales, por lo que ninguna de las nuevas intercalaciones tiene (o necesita) la marca SC.

Estas intercalaciones se admiten en los índices de Motor de base de datos, las tablas optimizadas para memoria, los índices de almacén de columnas y los módulos compilados de forma nativa.
    
##  <a name="Related_Tasks"></a> Tareas relacionadas    
    
|Tarea|Tema|    
|----------|-----------|    
|Describe cómo establecer o cambiar la intercalación de la instancia de SQL Server.|[Configurar o cambiar la intercalación del servidor](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|Describe cómo establecer o cambiar la intercalación de una base de datos de usuario.|[Establecer o cambiar la intercalación de base de datos](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|Describe cómo establecer o cambiar la intercalación de una columna de la base de datos.|[Establecer o cambiar la intercalación de columnas](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|Describe cómo devolver información de intercalación en el servidor, la base de datos, o el nivel de columna.|[Ver información de intercalación](../../relational-databases/collations/view-collation-information.md)|    
|Describe cómo escribir instrucciones Transact-SQL que sean más portátiles de un idioma a otro, o que admitan varios idiomas más fácilmente.|[Escribir instrucciones Transact-SQL internacionales](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|Describe cómo cambiar el idioma de la sesión permite cambiar el idioma de los mensajes de error y las preferencias acerca de cómo usar y mostrar los datos de fecha, hora y divisa.|[Establecer un idioma de la sesión](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> Contenido relacionado    
 [Prácticas recomendadas para cambiar las intercalaciones en SQL Server](http://go.microsoft.com/fwlink/?LinkId=113891)    
    
 ["Migración de las prácticas recomendadas de SQL Server a Unicode"](http://go.microsoft.com/fwlink/?LinkId=113890)    
    
 [Sitio web de Unicode Consortium](http://go.microsoft.com/fwlink/?LinkId=48619)    
    
## <a name="see-also"></a>Consulte también    
 [Intercalaciones de bases de datos independientes](../../relational-databases/databases/contained-database-collations.md)     
 [Elegir un idioma al crear un índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)    
    
  

