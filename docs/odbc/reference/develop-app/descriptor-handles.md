---
title: Identificadores de descriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3aa085cc0a098f557ca7a8cbddcd787a178b79d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760770"
---
# <a name="descriptor-handles"></a>Identificadores de descriptor
Un *descriptor* es una colección de metadatos que describen los parámetros de una instrucción SQL o las columnas del conjunto de resultados, tal como se muestra la aplicación o controlador (también conocido como el *implementación*). Por lo tanto, puede rellenar un descriptor de cualquiera de las cuatro funciones:  
  
-   **Descriptor de parámetro de la aplicación (APD).** Contiene información acerca de los búferes de la aplicación enlazada a los parámetros en una instrucción SQL, como sus direcciones, las longitudes y tipos de datos C.  
  
-   **Descriptor de parámetro de implementación (IPD).** Contiene información sobre los parámetros en una instrucción SQL, como sus tipos de datos SQL, las longitudes y nulabilidad.  
  
-   **Descriptor de fila de la aplicación (descartar).** Contiene información acerca de los búferes de aplicación enlazadas a las columnas en un conjunto de resultados, como sus direcciones, las longitudes y tipos de datos C.  
  
-   **Descriptor de fila de implementación (IRD).** Contiene información acerca de las columnas en un conjunto de resultados, como sus tipos de datos SQL, las longitudes y nulabilidad.  
  
 Los descriptores de cuatro (cada rol relleno uno) se asignan automáticamente cuando se asigna a una instrucción. Estos se conocen como *asigna automáticamente los descriptores de* y siempre están asociadas con esa instrucción. Las aplicaciones también pueden asignar los descriptores con **SQLAllocHandle**. Estos se conocen como *asigna explícitamente los descriptores de*. Que se asignan en una conexión y se pueden asociar con una o varias instrucciones en esa conexión para cumplir la función de un APD o descartar en esas instrucciones.  
  
 Mayoría de las operaciones en ODBC puede realizarse sin uso explícito de descriptores de la aplicación. Sin embargo, los descriptores de proporcionan un acceso directo conveniente para algunas operaciones. Por ejemplo, suponga que una aplicación que desea insertar los datos de dos conjuntos diferentes de los búferes. Para usar el primer conjunto de búferes, llamaría a repetidamente **SQLBindParameter** para enlazarlos a los parámetros de un **insertar** instrucción y, a continuación, ejecute la instrucción. Para usar el segundo conjunto de búferes, debería repetir este proceso. Como alternativa, podría configurar enlaces para el primer conjunto de búferes en un descriptor y el segundo conjunto de búferes en otro descriptor. Para cambiar entre los conjuntos de enlaces, la aplicación llamaría simplemente **SQLSetStmtAttr** y asociar el descriptor correcto con la instrucción como el APD.  
  
 Para obtener más información acerca de los descriptores, consulte [tipos de descriptores](../../../odbc/reference/develop-app/types-of-descriptors.md).
