---
description: Definición del formato de serialización de secuencias de DCOM
title: Estableciendo el formato de serialización de secuencia DCOM | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 47e581ec9bd3ee04af7e8f4400e3636ddc22bd37
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451987"
---
# <a name="setting-dcom-stream-marshaling-format"></a>Definición del formato de serialización de secuencias de DCOM
Un equipo cliente que usa componentes de RDS 1,5 o anterior no es compatible con un servidor que usa componentes de RDS 2,0 o posterior. Al utilizar DCOM como el protocolo subyacente, la compatibilidad con RDS 2,0 o posterior es más eficaz en el transporte de objetos de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) . Si el cliente ejecuta componentes de RDS 1,5 o anterior, puede configurar el servidor para que funcione con la compatibilidad de RDS anterior (denominada RDS 1,0) o con la compatibilidad de RDS más reciente (denominada RDS 2,0 o posterior). Establezca una de las siguientes entradas del registro:  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 o bien  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


