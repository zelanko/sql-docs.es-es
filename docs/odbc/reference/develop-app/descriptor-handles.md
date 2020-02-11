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
ms.openlocfilehash: 24e3d4c87f3bc461a339a6cb635d64f20dc73e20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106164"
---
# <a name="descriptor-handles"></a>Identificadores de descriptor
Un *descriptor* es una colección de metadatos que describe los parámetros de una instrucción SQL o las columnas de un conjunto de resultados, tal como la muestra la aplicación o el controlador (también conocido como *implementación*). Por lo tanto, un descriptor puede rellenar cualquiera de los cuatro roles siguientes:  
  
-   **Descriptor de parámetros de aplicación (APD).** Contiene información acerca de los búferes de aplicación enlazados a los parámetros de una instrucción SQL, como sus direcciones, longitudes y tipos de datos de C.  
  
-   **Descriptor de parámetros de implementación (IPD).** Contiene información sobre los parámetros de una instrucción SQL, como sus tipos de datos SQL, longitudes y nulabilidad.  
  
-   **Descriptor de fila de aplicación (ARD).** Contiene información acerca de los búferes de aplicación enlazados a las columnas de un conjunto de resultados, como sus direcciones, longitudes y tipos de datos de C.  
  
-   **Descriptor de fila de implementación (IRD).** Contiene información sobre las columnas de un conjunto de resultados, como sus tipos de datos SQL, longitudes y nulabilidad.  
  
 Cuando se asigna una instrucción, se asignan automáticamente cuatro descriptores (uno que rellenan cada rol). Estos se conocen como *descriptores asignados automáticamente* y siempre se asocian a esa instrucción. Las aplicaciones también pueden asignar descriptores con **SQLAllocHandle**. Estos se conocen como *descriptores asignados explícitamente*. Se asignan en una conexión y se pueden asociar a una o varias instrucciones de esa conexión para cumplir el rol de APD o ARD en esas instrucciones.  
  
 La mayoría de las operaciones de ODBC se pueden realizar sin el uso explícito de los descriptores de la aplicación. Sin embargo, los descriptores proporcionan un acceso directo cómodo para algunas operaciones. Por ejemplo, supongamos que una aplicación desea insertar datos de dos conjuntos diferentes de búferes. Para usar el primer conjunto de búferes, llamaría repetidamente a **SQLBindParameter** para enlazarlos a los parámetros en una instrucción **Insert** y, a continuación, ejecutar la instrucción. Para usar el segundo conjunto de búferes, se repetiría este proceso. Como alternativa, podría configurar enlaces al primer conjunto de búferes de un descriptor y al segundo conjunto de búferes de otro descriptor. Para cambiar entre los conjuntos de enlaces, la aplicación simplemente llamaría a **SQLSetStmtAttr** y asociara el descriptor correcto con la instrucción como APD.  
  
 Para obtener más información acerca de los descriptores, vea [tipos de descriptores](../../../odbc/reference/develop-app/types-of-descriptors.md).
