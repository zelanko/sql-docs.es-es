---
title: Optimización de la base de datos mediante carga de trabajo del Almacén de consultas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, Query Store
ms.assetid: 17107549-5073-4fa2-8ee7-5ed33b38821e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 4abca73a7d1ac259034987a494f5d7395b507a3a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68113171"
---
# <a name="tuning-database-using-workload-from-query-store"></a>Optimización de la base de datos mediante carga de trabajo del Almacén de consultas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


La característica [Almacén de consultas](../../relational-databases/performance/how-query-store-collects-data.md) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] captura de forma automática un historial de las consultas, planes y estadísticas de tiempo de ejecución, y almacena esta información en la base de datos. El [Asistente para la optimización del motor de base de datos (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) es compatible con una nueva opción para usar el Almacén de consultas para seleccionar automáticamente una carga de trabajo adecuada para la optimización. Para muchos usuarios, esto puede evitar la necesidad de recopilar explícitamente una carga de trabajo para la optimización. Esta característica solo está disponible si la base de datos tiene activada la característica Almacén de consultas. 
  
Esta característica está disponible con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **v16.4** o superior. 
  
## <a name="how-to-tune-a-workload-from-query-store-in-database-engine-tuning-advisor-gui"></a>Cómo optimizar una carga de trabajo del Almacén de consultas en la GUI del Asistente para la optimización de motor de base de datos
En la interfaz gráfica de usuario del DTA, seleccione el botón de radio **Almacén de consultas** del panel **General** para habilitar esta característica (vea la figura siguiente).

![Carga de trabajo de DTA del almacén de consultas](../../relational-databases/performance/media/dta-workload-from-query-store.gif)
 
## <a name="how-to-tune-a-workload-from-query-store-in-dtaexe-command-line-utility"></a>Cómo optimizar una carga de trabajo del Almacén de consultas en la utilidad de línea de comandos dta.exe
Desde la línea de comandos (dta.exe), elija la opción **-iq** para seleccionar la carga de trabajo del Almacén de consultas. 

Hay dos opciones adicionales disponibles a través de la línea de comandos que ayudan a optimizar el comportamiento del DTA al seleccionar la carga de trabajo en el Almacén de consultas. Estas opciones no están disponibles a través de la interfaz gráfica de usuario:
  1. **Número de eventos de carga de trabajo para optimizar**: esta opción, especificada mediante el argumento de línea de comandos **-n**, permite al usuario controlar el número de eventos del Almacén de consultas que se optimizan. De forma predeterminada, DTA usa un valor de 1000 para esta opción. Tenga en cuenta que DTA siempre elige los eventos más costosos por duración total. 
  
  2. **Ventanas de tiempo de los eventos que se van a optimizar**: como el almacén de consultas puede contener consultas que se han ejecutado hace mucho tiempo, esta opción permite al usuario especificar una ventana de tiempo pasada (en horas) en la que es necesario que se ejecute una consulta para que DTA la considere para la optimización. Esta opción se especifica con el argumento de línea de comandos **-I**. 

Para obtener más información, vea [dta (utilidad)](../../tools/dta/dta-utility.md).

## <a name="difference-between-using-workload-from-query-store-and-plan-cache"></a>Diferencia entre el uso de la carga de trabajo del Almacén de consultas y la caché de planes 
La diferencia entre las opciones Almacén de consultas y caché de planes es que la primera contiene un historial más extenso de consultas que se han ejecutado en la base de datos, guardadas entre reinicios del servidor. Por otro lado, la caché de planes solo contiene un subconjunto de consultas ejecutadas recientemente cuyos planes se almacenan en caché en memoria. Cuando se reinicia el servidor, se descartan las entradas en la caché de planes.

## <a name="see-also"></a>Consulte también  
[Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)     
[Tutorial: Asistente para la optimización de motor de base de datos](../../tools/dta/tutorial-database-engine-tuning-advisor.md)        
[Introducción a la recopilación de datos del almacén de consultas](../../relational-databases/performance/how-query-store-collects-data.md)     
[Almacén de consultas, procedimientos recomendados](../../relational-databases/performance/best-practice-with-the-query-store.md)
