---
title: "Archivos DLL de instalación de traductor | Documentos de Microsoft"
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
helpviewer_keywords: translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cd4f8ef7edac4894ee676a0ae5d4cdc95a615fab
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="translator-setup-dlls"></a>Archivos DLL de instalación de traductor
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo de Windows. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 El programa de instalación de traductor DLL contiene la **ConfigTranslator** función, que devuelve la opción predeterminada para un traductor. Si es necesario, pide al usuario esta información. Para obtener una descripción completa de esta función, consulte [referencia de API de DLL de instalación](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 El programa de instalación de traductor archivo DLL está escrito por el programador de traductor. Puede ser parte del traductor de DLL o un archivo DLL independiente.
