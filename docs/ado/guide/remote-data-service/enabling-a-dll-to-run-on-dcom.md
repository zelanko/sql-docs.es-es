---
title: Habilitar una DLL para que se ejecute en DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ea7ea83219780602f8d8d68e5c807178e775bc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922700"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Habilitación de un archivo DLL para ejecutarlo en DCOM
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 En los pasos siguientes se describe cómo habilitar un objeto Business. dll para usar DCOM y Microsoft Internet Information Services (HTTP) a través de servicios de componentes.  
  
1.  Cree un nuevo paquete vacío en el complemento MMC servicios de componentes.  
  
     Usará el complemento MMC servicios de componentes para crear un paquete y agregar el archivo DLL a este paquete. Esto hace que el archivo. dll sea accesible a través de DCOM, pero quita la accesibilidad a través de IIS. (Si protege el registro para el archivo. dll, la clave **Inproc** está ahora vacía; al establecer el atributo de activación, que se explica más adelante en este tema, se agrega un valor en la clave **Inproc** ).  
  
2.  Instale un objeto comercial en el paquete.  
  
     O bien  
  
     Importe el objeto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) en el paquete.  
  
3.  Establezca el atributo de activación del paquete **en en el proceso del creador** (aplicación de biblioteca).  
  
     Para que el archivo. dll sea accesible a través de DCOM e IIS en el mismo equipo, debe establecer el atributo de activación del componente en el complemento MMC servicios de componentes. Después de establecer el atributo en **en el proceso del creador**, observará que se ha agregado una clave de servidor **Inproc** en el registro que señala a un archivo. dll suplente de servicios de componentes.  
  
 Para obtener más información acerca de los servicios de componentes (o del servicio de transacciones de Microsoft, si usa Windows NT) y cómo realizar estos pasos, visite el sitio web del servidor de transacciones de Microsoft.


