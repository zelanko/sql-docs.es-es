---
title: "Utilizar relaciones de valor en un dominio compuesto | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dm.cdvaluerelations.f1"
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
caps.latest.revision: 12
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 12
---
# Utilizar relaciones de valor en un dominio compuesto
  En este tema se describe cómo ver las combinaciones de valores encontradas para el dominio compuesto durante el proceso de detección de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta página muestra el número de repeticiones de las combinaciones de valores. La administración de valores no se admite en los dominios compuestos, por lo que no se puede realizar ninguna operación con estos valores.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para ver las relaciones de valor, debe haber creado y abierto un dominio compuesto.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para ver las relaciones de valor de un dominio compuesto.  
  
##  <a name="Use"></a> Ver las relaciones de valor  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación de cliente de calidad de datos](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra o cree una base de conocimiento. Seleccione **Administración de dominios** como actividad y, a continuación, haga clic en **Abrir** o en **Crear**. Para obtener más información, consulte [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) o [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
3.  En la **Lista de dominios** de la página **Administración de dominios** , seleccione el dominio compuesto para el que desea crear una regla de dominio, o cree un nuevo dominio compuesto. Si necesita crear un nuevo dominio, vea [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
4.  Haga clic en la pestaña **Relaciones de valor** .  
  
5.  Vea las frecuencias mostradas para cada combinación de valores.  
  
    > [!NOTE]  
    >  La tabla **Valor** muestra las combinaciones de valores existentes en el dominio compuesto. Cada uno de los valores se muestra en el dominio individual al que se aplica. La ordenación predeterminada de la tabla de relaciones es por frecuencia, pero puede hacer clic en otra columna para ordenar por dicha columna. Solo se muestran aquellos valores con una frecuencia mayor o igual que 20.  
  
6.  No se puede cambiar ninguno de los valores de la tabla. Si ha realizado otras operaciones, haga clic en **Finalizar** para completar la actividad de administración de dominios. En caso contrario, haga clic en **Cancelar**.  
  
##  <a name="FollowUp"></a> Seguimiento: después de ver las relaciones de valor  
 Una vez vistas las relaciones de valor, puede realizar otras tareas de administración en el dominio, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para obtener más información, consulte [realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [administrar un dominio](../data-quality-services/managing-a-domain.md), o [crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
  