---
title: Descripción del bloqueo de fila | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cdf5ca943ec4d823c8c568f0818a49c44f22cbe6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040783"
---
# <a name="understanding-row-locking"></a>Descripción del bloqueo de filas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa bloqueos de fila de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos implementan el control de la simultaneidad entre varios usuarios que realizan modificaciones en una base de datos al mismo tiempo. De forma predeterminada, las transacciones y bloqueos se administran para cada conexión. Por ejemplo, si una aplicación abre dos conexiones JDBC, los bloqueos que una conexión adquiere no se pueden compartir con la otra. Ninguna conexión puede adquirir bloqueos que estarían en conflicto con los bloqueos contenidos en la otra conexión.  
  
> [!NOTE]  
>  Si se utiliza el bloqueo de filas, se bloquean todas las filas en el búfer de captura, por lo que si se establece un valor muy grande como tamaño de la lectura, se puede afectar a la simultaneidad.  
  
 El bloqueo se utiliza para asegurar la integridad transaccional y la coherencia de las bases de datos. El bloqueo evita que los usuarios lean datos que otros usuarios estén cambiado y que varios usuarios cambien al mismo tiempo los mismos datos. Si no se utilizan bloqueos, los datos dentro de la base de datos podrían llegar a ser lógicamente incorrectos y las consultas de esos datos podrían generar resultados inesperados.  
  
> [!NOTE]  
>  Para obtener más información sobre el bloqueo de fila en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], vea "Bloqueos en [!INCLUDE[ssDE](../../includes/ssde_md.md)]" en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Administrar conjuntos de resultados con el controlador JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
