---
title: La biblioteca de cursores ODBC (ODBC Cursor Library) Microsoft Docs
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
ms.openlocfilehash: b243e8ae2dc931830a249d4392da308e68722cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300055"
---
# <a name="the-odbc-cursor-library"></a>La biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Los cursores de bloque y desplazables son adiciones muy útiles a muchas aplicaciones. Sin embargo, no todos los controladores admiten cursores desplazables y de bloque. Lo mismo ocurre con las instrucciones update y delete posicionadas y **SQLSetPos**, que se describen en Actualización de datos. Por lo tanto, el componente ODBC del Windows SDK, que anteriormente se incluía en el SDK de Microsoft Data Access Components (MDAC), incluye una biblioteca de cursores. La biblioteca de cursores implementa bloques, cursores estáticos, instrucciones de actualización y eliminación posicionadas y **SQLSetPos** para cualquier controlador que cumpla con el nivel de conformidad de la CLI de Open Group Standard. La biblioteca de cursores se puede redistribuir con aplicaciones ODBC; consulte el acuerdo de licencia en el SDK para obtener más información.  
  
 Para utilizar la biblioteca de cursores, una aplicación establece el atributo de conexión SQL_ATTR_ODBC_CURSORS antes de conectarse al origen de datos. Para obtener más información acerca de la biblioteca de cursores, vea [Apéndice F: Biblioteca](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)de cursores ODBC .
