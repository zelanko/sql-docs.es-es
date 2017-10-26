---
title: Identificadores de descriptor | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99b1b3dc2eabd38aea148ad5ba946d7dd0da857d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-handles"></a>Identificadores de descriptor
A *descriptor* es una colección de metadatos que describen los parámetros de una instrucción SQL o las columnas del conjunto de resultados, tal como se muestra por la aplicación o el controlador (también conocido como el *implementación*). Por lo tanto, puede rellenar un descriptor de cualquiera de las siguientes funciones:  
  
-   **Descriptor de parámetro de la aplicación (APD).** Contiene información acerca de los búferes de aplicación enlazados a los parámetros en una instrucción SQL, como sus direcciones, longitudes y tipos de datos C.  
  
-   **Descriptor de parámetro de implementación (IPD).** Contiene información acerca de los parámetros en una instrucción SQL, como sus tipos de datos SQL, longitud y nulabilidad.  
  
-   **Descriptor de fila de la aplicación (descartar).** Contiene información acerca de los búferes de aplicación enlazada a las columnas de un conjunto de resultados, como sus direcciones, longitudes y tipos de datos C.  
  
-   **Descriptor de fila de implementación (IRD).** Contiene información sobre las columnas de un conjunto de resultados, como sus tipos de datos SQL, longitud y nulabilidad.  
  
 Descriptores de cuatro (un relleno cada rol) se asignan automáticamente cuando se asigna una instrucción. Se conocen como *asigna automáticamente los descriptores de* y siempre están asociadas a esa instrucción. Las aplicaciones pueden asignar descriptores con **SQLAllocHandle**. Se conocen como *asigna explícitamente descriptores*. Que se asignan en una conexión y se pueden asociar con una o varias instrucciones en esa conexión para satisfacer el rol de un APD o descartar en esas instrucciones.  
  
 Mayoría de las operaciones en ODBC puede realizarse sin uso explícito de descriptores de la aplicación. Sin embargo, los descriptores de proporcionan un acceso directo conveniente para algunas operaciones. Por ejemplo, supongamos que desea que una aplicación insertar datos de dos conjuntos diferentes de búferes. Para usar el primer conjunto de búferes, repetidamente llamaría a **SQLBindParameter** para enlazarlos a los parámetros de un **insertar** instrucción y, a continuación, ejecute la instrucción. Para usar el segundo conjunto de búferes, debería repetir este proceso. Como alternativa, podría configurar enlaces para el primer conjunto de búferes de un descriptor y el segundo conjunto de búferes en otro descriptor. Para alternar entre los conjuntos de enlaces, llamaría simplemente la aplicación **SQLSetStmtAttr** y asociar el descriptor correcta con la instrucción como el APD.  
  
 Para obtener más información acerca de los descriptores, consulte [tipos de descriptores](../../../odbc/reference/develop-app/types-of-descriptors.md).

