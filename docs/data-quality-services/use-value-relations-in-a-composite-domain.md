---
title: Usar relaciones de valor en un dominio compuesto | Microsoft Docs
ms.custom: 
ms.date: 11/22/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21b9faf53229207a3f5f862dd1ecc79803c21119
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="use-value-relations-in-a-composite-domain"></a>Utilizar relaciones de valor en un dominio compuesto
  En este tema se describe cómo ver las combinaciones de valores encontradas para el dominio compuesto durante el proceso de detección de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta página muestra el número de repeticiones de las combinaciones de valores. La administración de valores no se admite en los dominios compuestos, por lo que no se puede realizar ninguna operación con estos valores.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para ver las relaciones de valor, debe haber creado y abierto un dominio compuesto.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para ver las relaciones de valor de un dominio compuesto.  
  
##  <a name="Use"></a> Ver las relaciones de valor  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra o cree una base de conocimiento. Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Abrir** o en **Crear**. Para obtener más información, consulte [Crear una base de conocimiento](../data-quality-services/create-a-knowledge-base.md) o [Abrir una base de conocimiento](../data-quality-services/open-a-knowledge-base.md).  
  
3.  En la **Lista de dominios** de la página **Administración de dominios** , seleccione el dominio compuesto para el que desea crear una regla de dominio, o cree un nuevo dominio compuesto. Si necesita crear un nuevo dominio, vea [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
4.  Haga clic en la pestaña **Relaciones de valor** .  
  
5.  Vea las frecuencias mostradas para cada combinación de valores.  
  
    > [!NOTE]  
    >  La tabla **Valor** muestra las combinaciones de valores existentes en el dominio compuesto. Cada uno de los valores se muestra en el dominio individual al que se aplica. La ordenación predeterminada de la tabla de relaciones es por frecuencia, pero puede hacer clic en otra columna para ordenar por dicha columna. Solo se muestran aquellos valores con una frecuencia mayor o igual que 20.  
  
6.  No se puede cambiar ninguno de los valores de la tabla. Si ha realizado otras operaciones, haga clic en **Finalizar** para completar la actividad de administración de dominios. En caso contrario, haga clic en **Cancelar**.  
  
##  <a name="FollowUp"></a> Seguimiento: después de ver las relaciones de valor  
 Una vez vistas las relaciones de valor, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
  
