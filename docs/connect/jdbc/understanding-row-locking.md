---
title: Descripción del bloqueo de filas | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bcd18baf401378605abf0d53e203d0a3745ee887
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027336"
---
# <a name="understanding-row-locking"></a>Descripción del bloqueo de fila

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa bloqueos de fila de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos implementan controles de la simultaneidad entre varios usuarios que realizan modificaciones en una base de datos al mismo tiempo. De forma predeterminada, las transacciones y bloqueos se administran para cada conexión. Por ejemplo, si una aplicación abre dos conexiones JDBC, los bloqueos que una conexión adquiere no se pueden compartir con la otra. Ninguna conexión puede adquirir bloqueos que estarían en conflicto con los bloqueos contenidos en la otra conexión.

> [!NOTE]  
> Si se utiliza el bloqueo de filas, se bloquean todas las filas en el búfer de captura, por lo que si se establece un valor muy grande como tamaño de la lectura, se puede afectar a la simultaneidad.

El bloqueo se utiliza para asegurar la integridad transaccional y la coherencia de las bases de datos. El bloqueo evita que los usuarios lean datos que otros usuarios estén cambiado y que varios usuarios cambien al mismo tiempo los mismos datos. Si no se utilizan bloqueos, los datos dentro de la base de datos podrían llegar a ser lógicamente incorrectos y las consultas de esos datos podrían generar resultados inesperados.

> [!NOTE]  
> Para obtener más información sobre el bloqueo de fila en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Bloqueos en [!INCLUDE[ssDE](../../includes/ssde_md.md)]" en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Vea también

[Administración de conjuntos de resultados con el controlador JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)
