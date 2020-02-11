---
title: 'Caso práctico: creación de un ecosistema empresarial con Microsoft Dynamics ERP y SQL Server 2014 replicación para escalabilidad y rendimiento | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 2b0b5ab7-4e08-431a-bd59-360177c4565c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6cc9530b636409864e7e1b72f7417619a0fc8af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67792466"
---
# <a name="case-study-building-an-enterprise-ecosystem-with-microsoft-dynamics-erp-and-sql-server-2014-replication-for-scalability-and-performance"></a>Caso práctico: creación de un ecosistema empresarial utilizando la replicación de SQL Server 2014 y Microsoft Dynamics ERP para aumentar la escalabilidad y el rendimiento

  **Resumen:** En este documento se tratan los siguientes escenarios:  
Cómo usar la replicación transaccional en SQL Server 2014 para distribuir las transacciones de clientes de Dynamics AX en varios nodos. Como los datos se mantienen en tiempo real en los nodos, la replicación transaccional proporciona redundancia de los datos, lo que aumenta la disponibilidad de estos e incluye los disponibles para poder realizar análisis de rendimiento más eficaces.  
Cómo entender los detalles relacionados con el uso de la replicación transaccional para crear ecosistemas empresariales de alta escalabilidad en Microsoft Dynamics ERP. Ofrezca un rendimiento y una escalabilidad elevados sin tener que personalizar las características integradas de AX.  
  
 La replicación transaccional se suele utilizar en los flujos de trabajo de servidor a servidor que requieren un alto rendimiento. Por ejemplo, en los siguientes escenarios: aumento de la escalabilidad y disponibilidad, informes y almacenamiento de datos, integración de datos heterogéneos y de datos de varios sitios, así como descarga de procesamiento por lotes. En estas notas del producto se describen un escenario diferenciado y modelos asociados en los que se utiliza la replicación transaccional en Microsoft Dynamics ERP. Asimismo, se explican los procedimientos recomendados y retos que hay que tener en cuenta cuando se plantea utilizar la replicación transaccional para crear soluciones empresariales específicas de sistemas de planificación de recursos empresariales (ERP), así como los análisis de rendimiento en diferentes fases.  
  
 Este contenido es adecuado para desarrolladores, arquitectos y administradores de bases de datos. Se da por hecho que los lectores de estas notas del producto tienen conocimientos básicos de SQL Server 2008, 2012 o 2014, así como experiencia en administración de bases de datos de SQL Server.  
  
 **Escritor:** Prabhakaran Sethuraman (PRAB), Microsoft  
  
 **Revisores técnicos:** Prabhakaran Sethuraman (PRAB), Microsoft; Santosh Padhy, Microsoft; Pavel Majstrov, Microsoft; Karthik Sankaranarayanan, Microsoft; Jon Acone, Microsoft; David Stahlkopf, Microsoft; Kent Oldenburger, Microsoft; Mandi Ohlinger, Microsoft; Jason Roth, Microsoft  
  
 **Publicado:** 2015 de octubre  
  
 **Se aplica a:** SQL Server 2008, SQL Server 2012 y SQL Server 2014  
  
 Para revisar el documento, descargue el  
        [Caso práctico: creación de un ecosistema empresarial con Microsoft Dynamics ERP y SQL Server 2014 replicación para escalabilidad y rendimiento](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/A%20Case%20Study%20Using%20Replication%20to%20Build%20an%20Enterprise%20Ecosystem%20in%20Microsoft%20Dynamics%20ERP%20for%20Scalability%20and%20Performance.docx) Documento de Word.  
  
  
