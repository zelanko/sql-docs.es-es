---
title: Asignación de caracteres de SQL Server y MySQL establece (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 94764ed6777b4310ebc38bbf8375089a0ac00c92
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776421"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Asignación de caracteres de SQL Server y MySQL establece (MySQLToSQL)
Juego de caracteres (juego de caracteres) se puede especificar para tipos de datos de caracteres, expresiones y literales de MySQL.  
  
## <a name="charset-mapping"></a>Asignación de conjunto de caracteres  
Asignación de conjunto de caracteres se define para cada conjunto de caracteres de MySQL y se usa durante la conversión de tipo de datos de caracteres. Especifica cómo convertir a tipos de datos de cadena de caracteres de un juego de caracteres determinado:  
  
-   En tipos de caracteres de SQL Server nacionales (NCHAR/NVARCHAR), o  
  
-   Para los tipos de caracteres de SQL Server normales (CHAR/VARCHAR)  
  
1.  **nacional** son tipos de datos de caracteres de base de datos de destino:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **regular** son tipos de datos de caracteres de base de datos de destino:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  Asignación de tipos solo permite la asignación a **national** tipos de datos de caracteres. Cuando los tipo de datos de MySQL caracteres se convierten según la asignación de tipos, se aplica la asignación de conjunto de caracteres.  
  
> [!NOTE]  
> Asignación de conjunto de caracteres puede definirse en cada nivel de nodo del explorador de objetos de metadatos y representan todos los juegos de caracteres leídos de MySQL.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Asignación de conjunto de caracteres en el nivel de nodo diferentes  
Asignación de conjunto de caracteres varía en los niveles de otro nodo, a saber:  
  
1.  En el nivel de nodo de metadatos de raíz  
  
2.  En la base de datos, categoría y nivel de nodos de objeto  
  
> [!NOTE]  
> La pestaña seleccionada para editar la asignación de conjunto de caracteres, contiene tres botones, independientemente de la asignación en el nivel de nodo diferentes.  
>   
> Estas sobrecargas son:  
>   
> 1.  **Se aplican:** aplica los cambios realizados por el usuario, se habilita solamente cuando Editar asignación de juego de caracteres y aún no ha guardado.  
> 2.  **Cancelar:** cancela los cambios realizados por el usuario. El botón obtiene habilitado cuando la asignación de conjunto de caracteres es editar pero no se guardan.  
> 3.  **Restablecer valores predeterminados:** restablece todas las asignaciones de valores predeterminados.  
  
1.  **Nivel de nodo de metadatos de raíz:** cuadrícula de asignación de conjunto de caracteres contiene cuadrícula de juego de caracteres con una columna independiente para cada conjunto de caracteres. Las columnas de la cuadrícula son:  
  
    1.  La primera columna de la cuadrícula denominada **nombre del juego de caracteres** contiene el nombre del juego de caracteres.  
  
    2.  La segunda se denomina **descripción de juego de caracteres** contiene la descripción de juego de caracteres.  
  
    3.  La tercera columna titulada **tipo de juego de caracteres de destino** contiene la configuración de asignación de conjunto de caracteres determinado. Los valores de esta columna son:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > Los valores predeterminados para una codificación de caracteres determinada tienen el prefijo '(predeterminado)' después de CHAR/VARCHAR o NCHAR o NVARCHAR.  
  
    La asignación de conjunto de caracteres entre la base de datos MySQL y la base de datos de destino en el nivel de nodo de metadatos de raíz se indica a continuación:  
  
    ||||  
    |-|-|-|  
    |**Nombre del juego de caracteres**|**Descripción de juego de caracteres**|**Tipo de conjunto de caracteres de destino (valor predeterminado)**|  
    |Big5|Chino tradicional Big5|NCHAR/NVARCHAR (valor predeterminado)|  
    |dec8|Europeo occidental de diciembre|CHAR/VARCHAR (valor predeterminado)|  
    |CP850|Europeo occidental DOS|CHAR/VARCHAR (valor predeterminado)|  
    |hp8|Europeo occidental de HP|CHAR/VARCHAR (valor predeterminado)|  
    |koi8r|KOI8-R Relcom ruso|CHAR/VARCHAR (valor predeterminado)|  
    |Latín 1|CP1252 oeste europeo|CHAR/VARCHAR (valor predeterminado)|  
    |Latin2|ISO 8859-2 Centroeuropeo|CHAR/VARCHAR (valor predeterminado)|  
    |swe7|7 bits sueco|CHAR/VARCHAR (valor predeterminado)|  
    |ASCII|US ASCII|CHAR/VARCHAR (valor predeterminado)|  
    |ujis|EUC-JP japonés|NCHAR/NVARCHAR (valor predeterminado)|  
    |SJIS|Japonés Shift-JIS|NCHAR/NVARCHAR (valor predeterminado)|  
    |Hebreo|ISO 8859-8 Hebreo|CHAR/VARCHAR (valor predeterminado)|  
    |tis620|TIS620 tailandés|CHAR/VARCHAR (valor predeterminado)|  
    |eucKR|Coreano EUC-KR|NCHAR/NVARCHAR (valor predeterminado)|  
    |koi8u|Ucraniano KOI8-U|CHAR/VARCHAR (valor predeterminado)|  
    |gb2312|GB2312 Chino simplificado|NCHAR/NVARCHAR (valor predeterminado)|  
    |Griego|ISO 8859-7 Griego|CHAR/VARCHAR (valor predeterminado)|  
    |CP 1250|Centroeuropeo de Windows|CHAR/VARCHAR (valor predeterminado)|  
    |GBK|GBK chino simplificado|NCHAR/NVARCHAR (valor predeterminado)|  
    |Latin5|ISO 8859-9 Turco|CHAR/VARCHAR (valor predeterminado)|  
    |armscii8|Armenio ARMSCII-8|CHAR/VARCHAR (valor predeterminado)|  
    |UTF8|Unicode UTF-8|NCHAR/NVARCHAR (valor predeterminado)|  
    |ucs2|Unicode UCS-2|NCHAR/NVARCHAR (valor predeterminado)|  
    |cp866|Ruso DOS|CHAR/VARCHAR (valor predeterminado)|  
    |keybcs2|DOS Kamenicky checo-eslovaco|CHAR/VARCHAR (valor predeterminado)|  
    |macce|Mac Centroeuropeo|CHAR/VARCHAR (valor predeterminado)|  
    |MacRoman|Europeo occidental de Mac|CHAR/VARCHAR (valor predeterminado)|  
    |cp852|Centro de DOS Europea|CHAR/VARCHAR (valor predeterminado)|  
    |Latin7|ISO 8859-13 Báltico|CHAR/VARCHAR (valor predeterminado)|  
    |CP 1251|Windows cirílico|CHAR/VARCHAR (valor predeterminado)|  
    |CP 1256|Árabe de Windows|CHAR/VARCHAR (valor predeterminado)|  
    |CP 1257|Windows Báltico|CHAR/VARCHAR (valor predeterminado)|  
    |binary|Juego de caracteres binarios pseudo|CHAR/VARCHAR (valor predeterminado)|  
    |geostd8|Georgiano GEOSTD8|CHAR/VARCHAR (valor predeterminado)|  
    |cp932|SJIS en japonés de Windows|NCHAR/NVARCHAR (valor predeterminado)|  
    |eucjpms|UJIS para japonés de Windows|NCHAR/NVARCHAR (valor predeterminado)|  
  
2.  **En la base de datos, categoría o niveles de nodos de objeto:** en el nivel de base de datos, categoría o nodos de objeto, cuadrícula de asignación de conjunto de caracteres contiene las mismas filas y en el nivel de nodo de metadatos de raíz, especialmente.:  
  
    1.  La primera columna de la cuadrícula titulada **nombre de conjunto de caracteres** contiene el nombre del juego de caracteres.  
  
    2.  La segunda columna titulada **caracteres establecer descripción** contiene la descripción de juego de caracteres.  
  
    3.  La única diferencia es que los valores de la tercera columna de la cuadrícula. La tercera columna titulada **tipo de datos de destino** contiene la configuración de asignación de conjunto de caracteres determinado. Los valores de la columna son:  
  
        -   Heredado (CHAR/VARCHAR o NCHAR o NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   En la asignación de conjunto de caracteres entre la base de datos MySQL y base de datos de destino en la base de datos, categoría y niveles de nodos de objeto, los valores predeterminados de una codificación de caracteres determinada en cada nivel que no sea raíz para la columna **tipo de datos de destino** debe ser 'heredado'.  
> -   En la cuadrícula, el valor **Inherited** se utiliza como sufijo con cualquiera '(CHAR/VARCHAR)' o '(NCHAR/NVARCHAR)' dependiendo de qué valor se heredó de primario por este conjunto de caracteres determinado.  
  
