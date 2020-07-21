---
title: 'Tutorial: Preparar el servidor para la replicación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6bc070d34bdc580eecb7f2ce0c35d277545f1281
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049072"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>Tutorial: Preparar el servidor para la replicación
  Es importante planificar la seguridad antes de configurar la topología de replicación. En este tutorial se muestra cómo proteger una topología de replicación y cómo configurar la distribución, que es el primer paso en la replicación de datos. Debe finalizar este tutorial antes que cualquiera de los otros tutoriales.  
  
> [!NOTE]  
>  Para replicar datos de forma segura entre servidores, debe implementar todas las recomendaciones de [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En este tutorial aprenderá a preparar un servidor de manera que la replicación se ejecute de forma segura con los privilegios mínimos. En la primera lección se muestra cómo crear cuentas de servicio de Windows utilizadas para ejecutar agentes de replicación. En la segunda lección se muestra cómo configurar la carpeta utilizada para generar y almacenar instantáneas de publicación. En la tercera lección se muestra cómo configurar la distribución y establecer permisos.  
  
## <a name="requirements"></a>Requisitos  
 Este tutorial está destinado a usuarios que están familiarizados con las operaciones básicas de las bases de datos, pero que tienen una experiencia limitada en operaciones de replicación.  
  
 Para utilizar este tutorial, el sistema debe tener instalados los siguientes componentes:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada.  
  
 **Tiempo estimado para completar este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lecciones de este tutorial  
  
-   [Lección 1: Creación de cuentas de Windows para replicación](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lección 2: Preparar la carpeta de instantáneas](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lección 3: Configurar la distribución](lesson-3-configuring-distribution.md)  
  
 [Inicio del tutorial](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>Consulte también  
 [Configurar la distribución](configure-distribution.md)   
 [Seguridad de Replicación de SQL Server](security/view-and-modify-replication-security-settings.md)  
  
  
