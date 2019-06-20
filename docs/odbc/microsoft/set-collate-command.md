---
title: Comando COLLATE SET | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 372d3b2df79d66084f5599b4ac098b8c273ee78a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127830"
---
# <a name="set-collate-command"></a>Comando COLLATE Set
Especifica una secuencia de intercalación para los campos de carácter en posteriores de indización y operaciones de ordenación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argumentos  
 *cSequenceName*  
 Especifica una secuencia de intercalación. Se describen las opciones de la secuencia de intercalación disponible en la tabla siguiente.  
  
|Opciones|Lenguaje|  
|-------------|--------------|  
|HOLANDÉS|Neerlandés|  
|GENERAL|Inglés, francés, alemán, español moderno, portugués y otros idiomas de Europa occidental|  
|ALEMÁN|Orden de alemán de libreta de teléfonos (DIN)|  
|ISLANDIA|Islandés|  
|MÁQUINA|Máquina (la secuencia de intercalación predeterminada para las versiones anteriores de FoxPro)|  
|NORDAN|Noruego, danés|  
|ESPAÑOL|Español tradicional|  
|SWEFIN|Sueco, finlandés|  
|UNIQWT|Peso único|  
  
> [!NOTE]  
>  Cuando se especifica la opción español, *ch* es una letra única que ordena entre *c* y *d.* , y *ll* ordena entre  *l* y *m*.  
  
 Si especifica una opción de secuencia de intercalación como una cadena de caracteres literales, asegúrese de encerrarlo entre comillas en la opción:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MÁQUINA es la opción de secuencia de intercalación predeterminada y está familiarizado con los usuarios de Xbase de secuencia. Caracteres se ordenan como aparecen en la página de códigos actual.  
  
 GENERAL puede ser preferible para los usuarios de Estados Unidos y Europa occidental. Caracteres se ordenan como aparecen en la página de códigos actual. En las versiones de FoxPro anteriores a la 2.5, los índices se haya creado mediante el **superior**() o **inferior**funciones () para convertir los campos de caracteres en un caso coherente. En versiones de FoxPro posteriores a la 2.5, en su lugar, puede especificar la opción de secuencia de intercalación GENERAL y omitir el **superior**conversión ().  
  
 Si especifica una opción de secuencia de intercalación distinta de la máquina y si se crea un archivo .idx, siempre se crea un .idx compact.  
  
 Utilice SET("COLLATE") para devolver la secuencia de intercalación actual.  
  
 Puede especificar una secuencia de intercalación para un origen de datos mediante el [cuadro de diálogo de instalación de Visual FoxPro de ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o mediante la palabra clave Collate en la cadena de conexión con [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Esto es idéntico al emitir el comando siguiente:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Comentarios  
 CONJUNTO de INTERCALACIONES permite a las tablas de orden que contiene los caracteres acentuados para cualquiera de los idiomas admitidos. Cambiar la configuración de conjunto de INTERCALACIONES no afecta a la secuencia de intercalación de los índices abiertos previamente. Visual FoxPro mantiene automáticamente los índices existentes, que proporciona la flexibilidad necesaria para crear muchos tipos diferentes de los índices, incluso para el mismo campo.  
  
 Por ejemplo, si se crea un índice con el conjunto de INTERCALACIONES establecido en GENERAL y posteriormente se cambia la configuración de conjunto de INTERCALACIONES en español, el índice conserva la secuencia de intercalación GENERAL.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de configuración de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
