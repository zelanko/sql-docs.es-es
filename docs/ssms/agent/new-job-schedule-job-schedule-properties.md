---
title: Nueva programación de trabajo - Propiedades de programación del trabajo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.scheduleproperties.f1
- sql13.swb.maint.editrecurringjobsched.f1
ms.assetid: 5c0b1bc9-dd87-49cc-b0dd-75d0d922b177
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ace04d16e537e50c10e0eaa5c4fa432d1db7055f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245207"
---
# <a name="new-job-schedule---job-schedule-properties"></a>Nueva programación de trabajo - Propiedades de programación del trabajo
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice esta página para ver y cambiar las propiedades de la programación.  
  
## <a name="options"></a>Opciones  
**Nombre**  
Escriba un nuevo nombre de la programación.  
  
**Trabajos en programación**  
Vea los trabajos que utiliza la programación.  
  
**Tipo de programación**  
Seleccione el tipo de programación.  
  
**Enabled**  
Seleccione esta opción para habilitar o deshabilitar la programación.  
  
## <a name="recurring-schedule-types-options"></a>Opciones de tipos de programación periódica  
**Sucede**  
Seleccione el intervalo con el que se repite la programación.  
  
**Se repite cada**  
Seleccione el número de días o semanas entre las repeticiones de la programación. Esta opción no está disponible para las programaciones de periodicidad mensual.  
  
**Lunes**  
Configure el trabajo para que tenga lugar el lunes. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Martes**  
Configure el trabajo para que tenga lugar el martes. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Miércoles**  
Configure el trabajo para que tenga lugar el miércoles. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Jueves**  
Configure el trabajo para que tenga lugar el jueves. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Viernes**  
Configure el trabajo para que tenga lugar el viernes. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Sábado**  
Configure el trabajo para que tenga lugar el sábado. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Domingo**  
Configure el trabajo para que tenga lugar el domingo. Solo está disponible para las programaciones de periodicidad semanal.  
  
**Day**  
Seleccione el día del mes en el que se ejecutará la programación. Solo está disponible para las programaciones de periodicidad mensual.  
  
**de cada**  
Seleccione el número de meses entre las repeticiones de la programación. Solo está disponible para las programaciones de periodicidad mensual.  
  
**El**  
Especifique una programación para un día determinado de la semana, en un semana determinada del mes. Solo está disponible para las programaciones de periodicidad mensual.  
  
**Sucede una vez a las**  
Establezca la hora para que el trabajo se produzca diariamente.  
  
**Sucede cada**  
Establece el número de horas, minutos o segundos entre repeticiones.  
  
**Fecha de inicio**  
Establece la fecha en que comienza a ser efectiva esta programación.  
  
**Fecha de finalización**  
Establece la fecha en que deja de ser efectiva la programación.  
  
**Sin fecha de finalización**  
Especifica que la programación será efectiva indefinidamente.  
  
## <a name="one-time-schedule-types-options"></a>Opciones de tipos de programación de una sola vez  
**Date**  
Seleccione la fecha de ejecución del trabajo.  
  
**Time**  
Seleccione la hora de ejecución del trabajo.  
  
## <a name="see-also"></a>Consulte también  
[Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Programar un trabajo](../../ssms/agent/schedule-a-job.md)  
  
