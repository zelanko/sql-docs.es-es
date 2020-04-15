---
title: Manijas del descriptor ( Descriptor Handles) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0595c97f3f4ad92d976c89327a01e25cb5b753
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305916"
---
# <a name="descriptor-handles"></a>Identificadores de descriptor
Un *descriptor* es una colección de metadatos que describe los parámetros de una instrucción SQL o las columnas de un conjunto de resultados, como lo ve la aplicación o el controlador (también conocido como la *implementación).* Por lo tanto, un descriptor puede llenar cualquiera de los cuatro roles:  
  
-   **Descriptor de parámetros de aplicación (APD).** Contiene información sobre los búferes de aplicación enlazados a los parámetros de una instrucción SQL, como sus direcciones, longitudes y tipos de datos C.  
  
-   **Descriptor de parámetros de implementación (IPD).** Contiene información sobre los parámetros de una instrucción SQL, como sus tipos de datos SQL, longitudes y nulabilidad.  
  
-   **Descriptor de fila de aplicación (ARD).** Contiene información sobre los búferes de aplicación enlazados a las columnas de un conjunto de resultados, como sus direcciones, longitudes y tipos de datos De C.  
  
-   **Descriptor de fila de implementación (IRD).** Contiene información sobre las columnas de un conjunto de resultados, como sus tipos de datos SQL, longitudes y nulabilidad.  
  
 Cuatro descriptores (uno que rellena cada rol) se asignan automáticamente cuando se asigna una instrucción. Estos se conocen como *descriptores asignados automáticamente* y siempre se asocian a esa instrucción. Las aplicaciones también pueden asignar descriptores con **SQLAllocHandle**. Estos se conocen como *descriptores asignados explícitamente.* Se asignan en una conexión y se pueden asociar con una o más instrucciones en esa conexión para cumplir el rol de un APD o ARD en esas declaraciones.  
  
 La mayoría de las operaciones en ODBC se pueden realizar sin el uso explícito de descriptores por parte de la aplicación. Sin embargo, los descriptores proporcionan un acceso directo conveniente para algunas operaciones. Por ejemplo, supongamos que una aplicación desea insertar datos de dos conjuntos diferentes de búferes. Para usar el primer conjunto de búferes, llamaría repetidamente **SQLBindParameter** para enlazarlos a los parámetros de una instrucción **INSERT** y, a continuación, ejecutar la instrucción. Para utilizar el segundo conjunto de búferes, repetiría este proceso. Como alternativa, podría configurar enlaces al primer conjunto de búferes en un descriptor y al segundo conjunto de búferes en otro descriptor. Para cambiar entre los conjuntos de enlaces, la aplicación simplemente llamaría a **SQLSetStmtAttr** y asociaría el descriptor correcto con la instrucción como el APD.  
  
 Para obtener más información acerca de los descriptores, vea [Tipos de descriptores](../../../odbc/reference/develop-app/types-of-descriptors.md).
