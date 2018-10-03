---
title: Transacciones de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b1057dd8a7e70dc663d1b0de7d206fd7cc84e2c5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129915"
---
# <a name="integration-services-transactions"></a>Transacciones de Integration Services
  Los paquetes utilizan transacciones para enlazar las acciones de base de datos que las tareas realizan en unidades atómicas y mantener de esta forma la integridad de los datos. Todos los tipos de contenedor de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (contenedores de paquetes, de bucles For y Foreach o de secuencias, y hosts de las tareas que encapsulan cada tarea, se pueden configurar para que utilicen transacciones. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona tres opciones para configurar transacciones: **NotSupported**, **Supported**y **Required**.  
  
-   **Required** indica que el contenedor inicia una transacción, a menos que el contenedor principal ya haya iniciado otra. Si ya existe una transacción, el contenedor la combina. Por ejemplo, si un paquete que no está configurado para admitir transacciones, incluye un contenedor de secuencias que utiliza la opción **Required** , el contenedor de secuencias iniciará su propia transacción. Si el paquete se hubiera configurado para utilizar la opción **Required** , el contenedor de secuencias combinaría la transacción del paquete.  
  
-   **Supported** indica que el contenedor no inicia una transacción, pero sí combina cualquier transacción iniciada por el contenedor principal. Por ejemplo, si un paquete con cuatro tareas Ejecutar SQL inicia una transacción y las cuatro tareas utilizan la opción **Supported** , las actualizaciones de la base de datos realizadas por las tareas Ejecutar SQL se revierten si se produce un error en cualquiera de las tareas. Si el paquete no inicia una transacción, las cuatro tareas Ejecutar SQL no estarán enlazadas por una transacción y no se revertirá ninguna actualización de base de datos, excepto las realizadas por la tarea que tuvo el error.  
  
-   **NotSupported** indica que el contenedor no inicia una transacción ni combina una transacción existente. Una transacción iniciada por un contenedor principal no afecta a los contenedores secundarios configurados de manera que no admitan transacciones. Por ejemplo, si un paquete está configurado para iniciar una transacción y un contenedor de bucles For del paquete utiliza la opción **NotSupported** , no se revertirá ninguna de las tareas del contenedor de bucles For aunque genere un error.  
  
 Para configurar transacciones, hay que establecer la propiedad TransactionOption en el contenedor. Puede establecer esta propiedad en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]o mediante programación.  
  
> [!NOTE]  
>  La propiedad `TransactionOption` tiene influencia sobre el hecho de que el valor de la propiedad `IsolationLevel` solicitada por un contenedor se aplique o no. Para obtener más información, vea la descripción de la `IsolationLevel` propiedad en el tema [establecer las propiedades de paquete](set-package-properties.md).  
  
### <a name="to-configure-a-package-to-use-transactions"></a>Para configurar un paquete para que utilice transacciones  
  
-   [Configurar un paquete para el uso de transacciones](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [Cómo usar transacciones en SQL Server Integration Services (SSIS)](http://go.microsoft.com/fwlink/?LinkId=157783)(en inglés), en www.mssqltips.com  
  
## <a name="see-also"></a>Vea también  
 [Transacciones heredadas](../../2014/integration-services/inherited-transactions.md)   
 [Varias transacciones](../../2014/integration-services/multiple-transactions.md)  
  
  
