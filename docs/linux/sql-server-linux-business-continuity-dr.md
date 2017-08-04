---
title: "Recuperación ante desastres para SQL Server en Linux | Documentos de Microsoft"
description: 
author: mihaelab
ms.author: mihaelab
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: c75717c8-c677-4033-8ca6-d0ac93aee04d
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 86f41971e06efb767dde336cf93f9224a204176d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="business-continuity-and-database-recovery-sql-server-on-linux"></a>Continuidad empresarial y base de datos de recuperación SQL Server en Linux

SQL Server en Linux permite a las organizaciones lograr una amplia gama de objetivos de acuerdo de nivel de servicio para dar cabida a distintos requisitos de negocios.

Las soluciones más sencillas aprovechan las tecnologías de virtualización para lograr un alto grado de resistencia frente a errores de nivel de host, la tolerancia a errores frente a errores de hardware, así como la elasticidad y la maximización de recursos. Estos sistemas pueden ejecutarse de forma local, en una nube privada o pública o entornos híbridos. La forma más sencilla de protección y recuperación ante desastres es la copia de seguridad de base de datos. Las soluciones simples disponibles en SQL Server de 2017 RC2 incluyen:

- **Conmutación por error VM**
    - Resistencia frente a errores de nivel de sistema operativo y de invitado
    - Eventos planificados y no planificado
    - Tiempo de inactividad mínimo para la aplicación de revisiones y actualizaciones
    - RTO en minutos


- [**Restauración y copia de seguridad de base de datos**](sql-server-linux-backup-and-restore-database.md) 
    - Protección contra la corrupción de datos accidentales o malintencionados
    - Protección de recuperación ante desastres
    - RTO en minutos, horas

Técnicas de recuperación ante desastres y alta disponibilidad estándares proporcionan protección de nivel de instancia combinada con una infraestructura de almacenamiento compartido confiable. Para SQL Server de 2017 RC2 estándar de alta disponibilidad incluye:

- [**Clúster de conmutación por error**](sql-server-linux-shared-disk-cluster-configure.md)
    - Protección de nivel de instancia
    - Conmutación por error y la detección de errores automático
    - Resistencia frente a errores de sistema operativo y SQL Server
    - RTO en segundos a minutos


## <a name="summary"></a>Resumen

SQL Server de 2017 RC2 en Linux incluye clústeres de conmutación por error y restauración, copia de seguridad y virtualización para admitir la recuperación ante desastres y alta disponibilidad. 
