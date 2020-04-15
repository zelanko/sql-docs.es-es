---
title: Comando SET COLLATE (SET COLLATE Command) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9c1dfd59c00ad0ac0b7bd8b8f1cdfccc84d9b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300895"
---
# <a name="set-collate-command"></a>Comando COLLATE Set
Especifica una secuencia de intercalación para los campos de caracteres en las operaciones de indexación y ordenación posteriores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argumentos  
 *cSequenceName*  
 Especifica una secuencia de intercalación. Las opciones de secuencia de intercalación disponibles se describen en la tabla siguiente.  
  
|Opciones|Idioma|  
|-------------|--------------|  
|Holandés|Neerlandés|  
|GENERAL|Inglés, francés, alemán, español moderno, portugués y otros idiomas de Europa occidental|  
|Alemán|Orden de la agenda alemana (DIN)|  
|Islandia|Islandés|  
|Máquina|Máquina (la secuencia de intercalación predeterminada para versiones anteriores de FoxPro)|  
|NORDAN|Noruego, Danés|  
|Español|Español Tradicional|  
|SWEFIN|Sueco, Finlandés|  
|UNIQWT|Peso único|  
  
> [!NOTE]  
>  Cuando se especifica la opción SPANISH, *ch* es una sola letra que se ordena entre *c* y *d*, y *ll* ordena entre *l* y *m*.  
  
 Si especifica una opción de secuencia de intercalación como una cadena de caracteres literales, asegúrese de incluir la opción entre comillas:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE es la opción de secuencia de intercalación predeterminada y es la secuencia con la que los usuarios de Xbase están familiarizados. Los caracteres se ordenan tal como aparecen en la página de códigos actual.  
  
 GENERAL puede ser preferible para los usuarios de EE. UU. y Europa Occidental. Los caracteres se ordenan tal como aparecen en la página de códigos actual. En las versiones de FoxPro anteriores a 2.5, es posible que los índices se hayan creado utilizando las funciones **UPPER**( ) o **LOWER**( ) para convertir los campos de caracteres en un caso coherente. En las versiones de FoxPro posteriores a 2.5, puede especificar la opción de secuencia de intercalación GENERAL y omitir la conversión **UPPER**( ).  
  
 Si especifica una opción de secuencia de intercalación distinta de MACHINE y crea un archivo .idx, siempre se crea un archivo .idx compacto.  
  
 Utilice SET("COLLATE") para devolver la secuencia de intercalación actual.  
  
 Puede especificar una secuencia de intercalación para un origen de datos mediante el cuadro de diálogo Configuración de [ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o mediante la palabra clave Collate de la cadena de conexión con [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Esto es idéntico a emitir el siguiente comando:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Observaciones  
 SET COLLATE le permite pedir tablas que contienen caracteres acentuados para cualquiera de los idiomas admitidos. Cambiar la configuración de SET COLLATE no afecta a la secuencia de intercalación de los índices abiertos anteriormente. Visual FoxPro mantiene automáticamente los índices existentes, lo que proporciona la flexibilidad para crear muchos tipos diferentes de índices, incluso para el mismo campo.  
  
 Por ejemplo, si se crea un índice con SET COLLATE establecido en GENERAL y el valor SET COLLATE se cambia posteriormente a SPANISH, el índice conserva la secuencia de intercalación GENERAL.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo de configuración de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
