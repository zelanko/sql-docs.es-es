---
description: La biblioteca de cursores ODBC
title: Biblioteca de cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e5e3a01633a19c4ae82596ba1e180c64bcce06c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487518"
---
# <a name="the-odbc-cursor-library"></a>La biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 Los cursores de bloque y desplazables son adiciones muy útiles para muchas aplicaciones. Sin embargo, no todos los controladores admiten cursores de bloque y desplazables. Lo mismo se aplica a las instrucciones Update y DELETE posicionadas y a **SQLSetPos**, que se describen en actualizar datos. Por lo tanto, el componente ODBC del Windows SDK, anteriormente incluido en el SDK de Microsoft Data Access Components (MDAC), incluye una biblioteca de cursores. La biblioteca de cursores implementa el bloque, los cursores estáticos, las instrucciones Update y DELETE posicionadas y **SQLSetPos** para cualquier controlador que cumpla el nivel de conformidad de la CLI estándar de grupo abierto. La biblioteca de cursores se puede redistribuir con aplicaciones ODBC; Vea el contrato de licencia en el SDK para obtener más información.  
  
 Para utilizar la biblioteca de cursores, una aplicación establece el atributo de conexión SQL_ATTR_ODBC_CURSORS antes de conectarse al origen de datos. Para obtener más información acerca de la biblioteca de cursores, vea [Apéndice F: biblioteca de cursores ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
