---
title: "Transacciones de Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contenedores [Integration Services], transacciones"
  - "transacciones [Integration Services], acerca de transacciones en paquetes"
  - "tareas [Integration Services], transacciones"
  - "transacciones [Integration Services]"
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
caps.latest.revision: 51
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Transacciones de Integration Services
  Los paquetes utilizan transacciones para enlazar las acciones de base de datos que las tareas realizan en unidades atómicas y mantener de esta forma la integridad de los datos. Todos los tipos de contenedor de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (contenedores de paquetes, de bucles For y Foreach o de secuencias, y hosts de las tareas que encapsulan cada tarea, se pueden configurar para que utilicen transacciones. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona tres opciones para configurar transacciones: **NotSupported**, **Supported**y **Required**.  
  
-   **Required** indica que el contenedor inicia una transacción, a menos que el contenedor principal ya haya iniciado otra. Si ya existe una transacción, el contenedor la combina. Por ejemplo, si un paquete que no está configurado para admitir transacciones, incluye un contenedor de secuencias que utiliza la opción **Required** , el contenedor de secuencias iniciará su propia transacción. Si el paquete se hubiera configurado para utilizar la opción **Required** , el contenedor de secuencias combinaría la transacción del paquete.  
  
-   **Supported** indica que el contenedor no inicia una transacción, pero sí combina cualquier transacción iniciada por el contenedor principal. Por ejemplo, si un paquete con cuatro tareas Ejecutar SQL inicia una transacción y las cuatro tareas utilizan la opción **Supported** , las actualizaciones de la base de datos realizadas por las tareas Ejecutar SQL se revierten si se produce un error en cualquiera de las tareas. Si el paquete no inicia una transacción, las cuatro tareas Ejecutar SQL no estarán enlazadas por una transacción y no se revertirá ninguna actualización de base de datos, excepto las realizadas por la tarea que tuvo el error.  
  
-   **NotSupported** indica que el contenedor no inicia una transacción ni combina una transacción existente. Una transacción iniciada por un contenedor principal no afecta a los contenedores secundarios configurados de manera que no admitan transacciones. Por ejemplo, si un paquete está configurado para iniciar una transacción y un contenedor de bucles For del paquete utiliza la opción **NotSupported** , no se revertirá ninguna de las tareas del contenedor de bucles For aunque genere un error.  
  
 Para configurar transacciones, hay que establecer la propiedad TransactionOption en el contenedor. Puede establecer esta propiedad en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]o mediante programación.  
  
> [!NOTE]  
>  La propiedad **TransactionOption** tiene influencia sobre el hecho de que el valor de la propiedad **IsolationLevel** solicitada por un contenedor se aplique o no. Para obtener más información, vea la descripción de la propiedad **IsolationLevel** en el tema [Establecer las propiedades de paquete](../integration-services/set-package-properties.md).  
  
### Para configurar un paquete para que utilice transacciones  
  
-   [Configurar un paquete para el uso de transacciones](../Topic/Configure%20a%20Package%20to%20Use%20Transactions.md)  
  
## Recursos externos  
  
-   Entrada de blog, [Cómo usar transacciones en SQL Server Integration Services (SSIS)](http://go.microsoft.com/fwlink/?LinkId=157783)(en inglés), en www.mssqltips.com  
  
## Vea también  
 [Transacciones heredadas](../Topic/Inherited%20Transactions.md)   
 [Varias transacciones](../Topic/Multiple%20Transactions.md)  
  
  