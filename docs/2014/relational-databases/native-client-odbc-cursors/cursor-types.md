---
title: Tipos de cursor | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e63cceadf80da13956ea576db50459279a251b51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114243"
---
# <a name="cursor-types"></a>Tipos de cursor
  ODBC define cuatro tipos de cursor admitidos por Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client. Estos cursores varían en su capacidad para detectar cambios en el conjunto de resultados y en los recursos consumen, como la memoria y el espacio de **tempdb**. Un cursor solamente puede detectar cambios en las filas cuando intenta volver a capturar estas filas; el origen de datos no dispone de ningún método para notificar al cursor los cambios en las filas actualmente capturadas. El nivel de aislamiento de transacción también afecta la capacidad de un cursor para detectar modificaciones que no se realizaron a través del cursor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite cuatro tipos de cursor ODBC:  
  
-   Los cursores de solo avance no admiten el desplazamiento; solo admiten la captura de filas en serie desde el inicio hasta el final del cursor.  
  
-   Los cursores estáticos se compilan **tempdb** cuando el cursor está abierto. Siempre muestran el conjunto de resultados tal como estaba al abrir el cursor. Nunca reflejan los cambios en los datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores estáticos son siempre de solo lectura. Dado que un cursor de servidor estático se compila como una tabla de trabajo en **tempdb**, el tamaño del conjunto de resultados del cursor no puede superar el tamaño de fila máximo permitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   En los cursores controlados por conjunto de claves, la pertenencia y el orden de las filas del conjunto de resultados se fijan al abrir el cursor. Los cambios en las columnas sin clave son visibles a través del cursor.  
  
-   Los cursores dinámicos son los opuestos a los cursores estáticos. Reflejan todas las modificaciones realizadas en las filas de su conjunto de resultados. Los valores de datos, el orden y la pertenencia de las filas del conjunto de resultados pueden cambiar con cada captura.  
  
## <a name="see-also"></a>Vea también  
 [Uso de cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  