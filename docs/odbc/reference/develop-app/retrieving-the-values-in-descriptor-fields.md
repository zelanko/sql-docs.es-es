---
title: Recuperar los valores de campos de Descriptor | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f865e8372ba50cf2e6ee2bcfcf24863284cdd31
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperar los valores de campos de Descriptor
Una aplicación puede llamar a **SQLGetDescField** para obtener un único campo de un registro del descriptor. **SQLGetDescField** da acceso a la aplicación a todos los campos de descriptor que se definen en ODBC y a los campos definidos por el controlador.  
  
 **SQLGetDescRec** se puede llamar para recuperar la configuración de varios campos de descriptor que influyen en el tipo de datos y el almacenamiento de datos de columna o parámetro.
