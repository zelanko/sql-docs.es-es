---
title: Establecer formato de serialización de Stream DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: adec8a50e6bcf0af25227e2e456f3f76692f6d67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704183"
---
# <a name="setting-dcom-stream-marshaling-format"></a>Definición del formato de serialización de secuencias de DCOM
Un equipo cliente mediante los componentes de RDS 1.5 o versiones anteriores no es compatible con un servidor mediante los componentes de RDS 2.0 o posterior. Cuando se utiliza DCOM como protocolo subyacente, la compatibilidad con RDS 2.0 o posterior es más eficaz en el transporte [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. Si el cliente se está ejecutando los componentes de RDS 1.5 o versiones anteriores, puede establecer el servidor para que funcione con el soporte técnico RDS anterior (denominada RDS 1.0) o la nueva compatibilidad RDS (denominada RDS 2.0 o posterior). Establezca cualquiera de las entradas del registro siguientes:  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -o bien-  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


