---
title: La biblioteca de cursores ODBC | Documentos de Microsoft
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
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6250d693414a9d63077bcc5e47438d847ae72ce
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="the-odbc-cursor-library"></a>La biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Bloque y los cursores desplazables son adiciones muy útiles para muchas aplicaciones. Sin embargo, no todos los controladores admiten bloque y los cursores desplazables. El mismo puede decirse de actualización posicionada e instrucciones delete y **SQLSetPos**, que se trata de actualizar los datos. Por lo tanto, el componente ODBC del SDK de Windows, anteriormente incluida en Microsoft Data Access Components (MDAC) SDK, incluye una biblioteca de cursores. La biblioteca de cursores implementa bloque, los cursores estáticos, actualización por posición y las instrucciones delete, y **SQLSetPos** para cualquier controlador que cumple el nivel de conformidad abierto CLI estándar de grupo. La biblioteca de cursores que se puede redistribuir con las aplicaciones ODBC; consulte el contrato de licencia en el SDK para obtener más información.  
  
 Para usar la biblioteca de cursores, una aplicación establece el atributo de conexión SQL_ATTR_ODBC_CURSORS antes de conectarse al origen de datos. Para obtener más información acerca de la biblioteca de cursores, vea [biblioteca de cursores ODBC Apéndice F:](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).

