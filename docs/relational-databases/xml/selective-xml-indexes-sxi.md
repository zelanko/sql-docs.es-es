---
title: "Índices XML selectivos (SXI) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 598ecdcd-084b-4032-81b2-eed6ae9f5d44
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8270991f406e6845cdbe4d19fd8bc58e57eb4b35
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="selective-xml-indexes-sxi"></a>Índices XML selectivos (SXI)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Los índices XML selectivos son otro tipo de índice XML disponible además de los índices XML normales. Los objetivos de la característica de índice XML selectivo son los siguientes:  
  
-   Mejorar el rendimiento de las consultas sobre datos XML almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Admitir una indización más rápida de cargas de trabajo grandes de datos XML.  
  
-   Mejorar la escalabilidad reduciendo los costos de almacenamiento de los índices XML.  
  
 La limitación principal de los índices XML normales es que indizan el documento XML completo. Este conduce a varias desventajas importantes, como el menor rendimiento de las consultas y el mayor costo de mantenimiento de los índices, que están relacionadas principalmente con los costos de almacenamiento del índice.  
  
 La característica de índice XML selectivo le permite promover solo ciertas rutas de acceso de los documentos XML al índice. En el momento de la creación del índice se evalúan estas rutas de acceso, y los nodos a los que señalan se dividen y se almacenan en una tabla relacional en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta característica emplea un algoritmo de asignación eficiente desarrollado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research en colaboración con el equipo del producto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este algoritmo asigna los nodos XML a una única tabla relacional, y consigue un rendimiento excepcional y solo necesita una cantidad modesta de espacio de almacenamiento.  
  
 La característica de índice XML selectivo también admite índices XML selectivos secundarios sobre nodos que se han indizado mediante un índice XML selectivo. Estos índices selectivos secundarios son eficaces y mejoran aún más el rendimiento de las consultas.  
  
##  <a name="benefits"></a> Ventajas de los índices XML selectivos  
 Los índices XML selectivos proporcionan las ventajas siguientes:  
  
1.  Rendimiento de consultas mejorado considerablemente sobre el tipo de datos XML para cargas típicos de consulta.  
  
2.  Menores requisitos de almacenamiento en comparación con los índices XML normales.  
  
3.  Menores costos de mantenimiento de índices en comparación con los índices XML normales.  
  
4.  No es necesario actualizar las aplicaciones para beneficiarse de los índices XML selectivos.  
  
  
##  <a name="compare"></a> Índices XML selectivos e índices XML principales  
  
> [!IMPORTANT]  
>  Cree un índice XML selectivo en lugar de un índice XML normal en la mayoría de los casos para mejorar el rendimiento y lograr un almacenamiento más eficiente.  
  
 Sin embargo, no se recomienda usar un índice XML selectivo cuando alguna de las condiciones siguientes sea verdadera:  
  
-   Asigne un gran número de rutas de acceso del nodo.  
  
-   Admita consultas para elementos desconocidos o elementos de una ubicación desconocida en la estructura del documento.  
  
  
##  <a name="example"></a> Ejemplo simple de un índice XML selectivo  
 Considere el siguiente fragmento XML como un documento XML de una tabla de aproximadamente 500.000 filas:  
  
```xml  
<book>  
    <created>2004-03-01</created>   
    <authors>Various</authors>  
    <subjects>  
        <subject>English wit and humor -- Periodicals</subject>  
        <subject>AP</subject>   
    </subjects>  
    <title>Punch, or the London Charivari, Volume 156, April 2, 1919</title>  
    <id>etext11617</id>  
</book>  
```  
  
 Crear un índice XML principal sobre tantas filas de este esquema simple lleva mucho tiempo. La consulta de estos datos también se resiente del hecho de que un índice XML principal no admite la indización selectiva.  
  
 Si solo necesita consultar estos datos sobre la ruta de acceso `/book/title` y la ruta de acceso `/book/subjects` , puede crear el índice XML selectivo siguiente:  
  
```sql  
CREATE SELECTIVE XML INDEX SXI_index  
ON Tbl(xmlcol)  
FOR   
(  
    pathTitle = '/book/title/text()' AS XQUERY 'xs:string',   
    pathAuthors = '/book/authors' AS XQUERY 'node()',  
    pathId = '/book/id' AS SQL NVARCHAR(100)  
)  
```  
  
 La instrucción anterior es un buen ejemplo de sintaxis de CREATE que se usa cuando se crea un índice XML selectivo. En la instrucción CREATE, primero debe proporcionar un nombre para el índice e identificar la tabla y la columna XML para indizar. A continuación se proporcionan las rutas de acceso al índice. Una ruta de acceso consta de tres partes:  
  
1.  Un nombre que identifica de forma única la ruta de acceso.  
  
2.  Una expresión XQuery que describe la ruta de acceso.  
  
3.  Sugerencias opcionales de optimización.  
  
 Para obtener más información acerca de estos elementos, vea [Tareas relacionadas](#reltasks).  
  
  
## <a name="supported-features-prerequisites-and-limitations"></a>Características admitidas, requisitos previos y limitaciones  
  
###  <a name="features"></a> Características XML admitidas  
 Los índices XML selectivos admiten XQuery admitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de los métodos exist(), value() y nodes().  
  
-   Para los métodos exist(), value() y nodes(), los índices XML selectivos contienen información suficiente para transformar toda la expresión.  
  
-   En el caso de los métodos query() y modify(), los índices XML selectivos solo se pueden usar para el filtrado de nodos.  
  
-   Para el método query(), no se usan índices XML selectivos para recuperar resultados.  
  
-   Para el método modify(), no se usan índices XML selectivos para actualizar documentos XML.  
  
  
###  <a name="unsupported"></a> Características XML no admitidas  
 Los índices XML selectivos no admiten las siguientes características compatibles con la implementación de XML de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Indizar nodos con tipos XS complejos: tipos de unión, tipos de secuencia y tipos de lista.  
  
-   Indizar nodos con tipos XS binarios: por ejemplo, base64Binary y hexBinary.  
  
-   Especificar los nodos para indizar con expresiones Xpath que contienen el carácter comodín `*` al final. Por ejemplo,  `/a/b/c/*`, `/a//b/*`o `/a/b/*:c`.  
  
-   Indizar cualquier eje distinto de secundario, atributo o descendiente. El caso `//<step>` se permite como un caso especial.  
  
-   Indizar instrucciones de procesamiento y comentarios XML.  
  
-   Especificar y recuperar el identificador de un nodo mediante la función id().  
  
  
###  <a name="prereq"></a> Requisitos previos  
 Los siguientes requisitos previos deben existir antes de poder crear un índice XML selectivo en una columna XML en una tabla de usuario:  
  
-   Debe existir un índice clúster en la clave principal de la tabla de usuario.  
  
-   La clave principal de la tabla de usuario está limitada a un tamaño de 128 bytes cuando se usa con índices XML selectivos.  
  
-   La clave de agrupación de la tabla de usuario está limitada a 15 columnas cuando se usa con índices XML selectivos.  
  
  
###  <a name="limits"></a> Limitaciones  
 **Requisitos generales y limitaciones**  
  
-   Cada índice XML selectivo solamente puede crearse en una única columna XML.  
  
-   No puede crear un índice XML selectivo en una columna que no sea XML.  
  
-   Cada columna XML de una tabla solo puede tener un índice XML selectivo.  
  
-   Cada tabla puede tener hasta 249 índices XML selectivos.  
  
 **Limitaciones sobre objetos admitidos**  
  
 No puede crear índices XML selectivos en los objetos siguientes:  
  
1.  Columnas XML de una vista.  
  
2.  Variable con valores de tabla con columnas XML.  
  
3.  Variables de tipo XML.  
  
4.  Columnas XML calculadas.  
  
5.  Columnas XML con una profundidad de más de 128 nodos anidados.  
  
 **Limitaciones relativas al almacenamiento**  
  
 Hay un límite finito en cuanto al número de nodos del documento XML que se pueden agregar al índice. Un índice XML selectivo asigna documentos XML a una única tabla relacional. Por tanto, no puede tener más de 1024 columnas no NULL en ninguna fila especificada de la tabla. Además, muchas de las limitaciones de las columnas dispersas también se aplican a los índices XML selectivos, ya que los índices usan columnas dispersas para el almacenamiento.  
  
 El número máximo de columnas no NULL no admitidas en una fila determinada depende del tamaño de los datos de las columnas:  
  
-   En el mejor de los casos, se admiten 1024 columnas no NULL cuando todas las columnas son de tipo **bit**.  
  
-   En el peor de los casos, solo se admiten 236 columnas no NULL cuando todas las columnas son objetos grandes de tipo **varchar**.  
  
 Los índices XML selectivos usan de uno a cuatro columnas internamente para cada ruta de acceso del nodo que se indiza. El número total de nodos que se pueden indizar oscila desde 60 hasta varios cientos de nodos, según el tamaño real de los datos de las rutas de acceso indizadas.  
  
-   En el peor de los casos, cuando se asignan algunos o todos los nodos usando `//` en la definición de ruta de acceso del nodo, el número máximo de nodos indizados es 60.  
  
-   En el mejor de los casos, cuando se asignan nodos sin usar `//` en la definición de ruta de acceso del nodo, el número máximo de nodos indizados es 200.  
  
 **Los índices XML selectivos se vuelven a generar al crear (con CREATE) o modificar (con ALTER) el índice.**  
  
 Cuando usa CREATE o ALTER en un índice XML selectivo, se vuelve a generar en modo uniproceso sin conexión. Con frecuencia las instrucciones ALTER afectan negativamente al rendimiento de las consultas sobre los documentos XML indizados.  
  
 **Otras limitaciones**  
  
-   Los índices XML selectivos no se admiten en sugerencias de consulta.  
  
-   Los índices XML selectivos y los índices XML selectivos secundarios no se admiten en el Asistente para la optimización de base de datos.  
  
  
##  <a name="reltasks"></a> Tareas relacionadas  
  
|||  
|-|-|  
|**Tarea**|**Tema**|  
|Especificar las rutas de acceso del nodo que desea indizar y las sugerencias opcionales de optimización cuando cree o modifique un índice XML selectivo.|[Especificar rutas de acceso y sugerencias de optimización para índices XML selectivos](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)|  
|Crear, modificar o quitar un índice XML selectivo.|[Crear, modificar y quitar índices XML selectivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)|  
|Crear, modificar o quitar un índice XML selectivo secundario.|[Crear, modificar y quitar índices XML selectivos secundarios](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)|  
  
  
  
