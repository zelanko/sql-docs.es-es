---
title: Asignación de caracteres de SQL Server y MySQL (MySQLToSQL) de conjunto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cebdf2ed28287a59ec9d4f0daaa1d0c200f8fe20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312368"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Asignación de juegos de caracteres de MySQL y de SQL Server (MySQLToSQL)
Juego de caracteres (juego de caracteres) puede especificarse para los tipos de datos de caracteres, expresiones y literales de MySQL.  
  
## <a name="charset-mapping"></a>Asignación del juego de caracteres  
Asignación del juego de caracteres se define para cada juego de caracteres de MySQL y se usa durante la conversión de tipo de datos de caracteres. Especifica cómo convertir a tipos de datos de cadena de caracteres de un juego de caracteres determinado:  
  
-   A tipos de caracteres nacionales SQL Server (NCHAR o NVARCHAR), o  
  
-   Para tipos de caracteres de SQL Server normales (CHAR o VARCHAR)  
  
1.  **National** son tipos de datos de caracteres de base de datos de destino:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **regular** son tipos de datos de caracteres de base de datos de destino:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  Asignación de tipos solo permite la asignación a **nacional** tipos de datos de caracteres. Después de convertir el tipo de datos de caracteres de MySQL según la asignación de tipos, se aplica la asignación del juego de caracteres.  
  
> [!NOTE]  
> Asignación del juego de caracteres puede definirse en cada nivel de nodo del explorador de objetos de metadatos y representan todos los juegos de caracteres que leer de MySQL.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Asignación de juego de caracteres en los niveles de nodos diferente  
Asignación del juego de caracteres varía en los niveles de otro nodo, a saber:  
  
1.  En el nivel de nodo de metadatos de raíz  
  
2.  En la base de datos, categoría y nivel de nodos de objeto  
  
> [!NOTE]  
> La pestaña seleccionada para editar la asignación del juego de caracteres, contiene tres botones, con independencia de la asignación en los niveles de nodo diferente.  
>   
> Estas sobrecargas son:  
>   
> 1.  **Se aplican:** Aplica los cambios realizados por el usuario, se habilita solo cuando charset asignación editado y todavía no se han guardado.  
> 2.  **Cancelar:** Cancela los cambios realizados por el usuario. El botón se habilita cuando la asignación del juego de caracteres se modifica, pero no guardado.  
> 3.  **Restablecer valores predeterminados:** Restablece todas las asignaciones a los valores predeterminados.  
  
1.  **En el nivel de nodo de metadatos de raíz:**  Cuadrícula de asignación del juego de caracteres contiene cuadrícula de juego de caracteres con una columna independiente para cada juego de caracteres. Las columnas de la cuadrícula son:  
  
    1.  La primera columna de la cuadrícula denominada **nombre Charset** contiene el nombre del juego de caracteres.  
  
    2.  La otra denominada **Charset descripción** contiene la descripción de juego de caracteres.  
  
    3.  La tercera columna, titulada, **tipo de juego de caracteres de destino** contiene la configuración de asignación de conjunto de caracteres determinado. Los valores para esta columna son:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > Los valores predeterminados para un juego de caracteres determinado tienen el prefijo "(default)" después de CHAR/VARCHAR o NCHAR/NVARCHAR.  
  
    La asignación del juego de caracteres entre la base de datos de destino en el nivel de nodo de metadatos de raíz y de base de datos MySQL se indica a continuación:  
  
    ||||  
    |-|-|-|  
    |**Nombre del juego de caracteres**|**Descripción de juego de caracteres**|**Tipo de juego de caracteres de destino (valor predeterminado)**|  
    |big5|Chino tradicional Big5|NCHAR/NVARCHAR (valor predeterminado)|  
    |dec8|Europeo occidental Dic|CHAR o VARCHAR (valor predeterminado)|  
    |cp850|Europeo occidental de denegación de servicio|CHAR o VARCHAR (valor predeterminado)|  
    |hp8|HP West European|CHAR o VARCHAR (valor predeterminado)|  
    |koi8r|KOI8-R Relcom ruso|CHAR o VARCHAR (valor predeterminado)|  
    |Latín 1|Europeo occidental de CP1252|CHAR o VARCHAR (valor predeterminado)|  
    |Latin2|ISO 8859-2 Central European|CHAR o VARCHAR (valor predeterminado)|  
    |swe7|Sueco de 7 bits.|CHAR o VARCHAR (valor predeterminado)|  
    |ascii|ASCII DE EE. UU.|CHAR o VARCHAR (valor predeterminado)|  
    |ujis|EUC-JP japonés|NCHAR/NVARCHAR (valor predeterminado)|  
    |SJIS|Japonés Shift-JIS|NCHAR/NVARCHAR (valor predeterminado)|  
    |Hebreo|ISO 8859-8 Hebreo|CHAR o VARCHAR (valor predeterminado)|  
    |tis620|TIS620 tailandés|CHAR o VARCHAR (valor predeterminado)|  
    |euckr|Coreano EUC-KR|NCHAR/NVARCHAR (valor predeterminado)|  
    |koi8u|Ukrainian KOI8-U|CHAR o VARCHAR (valor predeterminado)|  
    |gb2312|GB2312 Chino simplificado|NCHAR/NVARCHAR (valor predeterminado)|  
    |Griego|ISO 8859-7 Griego|CHAR o VARCHAR (valor predeterminado)|  
    |cp 1250|Centroeuropeo de Windows|CHAR o VARCHAR (valor predeterminado)|  
    |gbk|GBK chino simplificado|NCHAR/NVARCHAR (valor predeterminado)|  
    |Latin5|ISO 8859-9 Turco|CHAR o VARCHAR (valor predeterminado)|  
    |armscii8|Armenio ARMSCII-8|CHAR o VARCHAR (valor predeterminado)|  
    |utf8|Unicode UTF-8|NCHAR/NVARCHAR (valor predeterminado)|  
    |ucs2|Unicode UCS-2|NCHAR/NVARCHAR (valor predeterminado)|  
    |cp866|Ruso de denegación de servicio|CHAR o VARCHAR (valor predeterminado)|  
    |keybcs2|Denegación de servicio Kamenicky checo-eslovaco|CHAR o VARCHAR (valor predeterminado)|  
    |macce|Centroeuropeo Mac|CHAR o VARCHAR (valor predeterminado)|  
    |MacRoman|Europeo occidental de Mac|CHAR o VARCHAR (valor predeterminado)|  
    |cp852|Denegación de servicio Central europea|CHAR o VARCHAR (valor predeterminado)|  
    |Latin7|ISO 8859-13 Báltico|CHAR o VARCHAR (valor predeterminado)|  
    |cp 1251|Windows Cyrillic|CHAR o VARCHAR (valor predeterminado)|  
    |cp 1256|Árabe de Windows|CHAR o VARCHAR (valor predeterminado)|  
    |cp 1257|Windows Báltico|CHAR o VARCHAR (valor predeterminado)|  
    |binary|Juego de caracteres binarios pseudo|CHAR o VARCHAR (valor predeterminado)|  
    |geostd8|Georgiano GEOSTD8|CHAR o VARCHAR (valor predeterminado)|  
    |cp932|SJIS en japonés de Windows|NCHAR/NVARCHAR (valor predeterminado)|  
    |eucjpms|UJIS en japonés de Windows|NCHAR/NVARCHAR (valor predeterminado)|  
  
2.  **En la base de datos, categoría o los niveles de nodos de objeto:** En el nivel de base de datos, categoría o nodos de objeto, cuadrícula de asignación del juego de caracteres contiene las mismas filas que del nivel raíz del nodo de metadatos, viz.:  
  
    1.  La primera columna de la cuadrícula titulada **nombre del conjunto de caracteres** contiene el nombre del juego de caracteres.  
  
    2.  La segunda columna, titulada, **carácter establecer descripción** contiene la descripción de juego de caracteres.  
  
    3.  La única diferencia es que los valores de la tercera columna de la cuadrícula. La tercera columna, titulada, **tipo de datos de destino** contiene la configuración de asignación de conjunto de caracteres determinado. Los valores de la columna son:  
  
        -   Heredado (CHAR/VARCHAR o NCHAR o NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   En la asignación del juego de caracteres entre la base de datos MySQL y base de datos de destino en la base de datos, categoría y los niveles de nodos de objeto, los valores predeterminados de un juego de caracteres determinada en cada nivel que no sea la raíz de la columna **tipo de datos de destino** debe ser ' Heredado '.  
> -   En la cuadrícula, el valor **Inherited** tiene el sufijo cualquiera '(CHAR/VARCHAR)' o '(NCHAR/NVARCHAR)' dependiendo de qué valor se hereda de primario por este juego de caracteres determinado.  
  
