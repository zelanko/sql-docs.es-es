---
title: Registro de paquetes con equilibrio de carga en servidores remotos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b45fa6607d6edc1559d8ebcbbbc7598e11eac408
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440292"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>Registro para la carga de paquetes equilibrados en servidores remotos
  Para un administrador es más fácil administrar los registros de todos los paquetes secundarios que están en ejecución en varios servidores cuando todos los paquetes secundarios utilizan el mismo proveedor de registro y todos escriben en el mismo destino. Una manera de crear un archivo común de registro para todos los paquetes secundarios es configurar los paquetes secundarios para que registren sus eventos en un proveedor de registro de SQL Server. Puede configurar todos los paquetes para que utilicen la misma base de datos, el mismo servidor y la misma instancia del servidor.  
  
 Para ver los archivos de registro, el administrador solo tiene que registrarse en un único servidor para ver los archivos de registro de todos los paquetes secundarios.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo habilitar el registro en un paquete, vea [Habilitar el registro de paquetes en SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md).  
  
## <a name="see-also"></a>Consulte también  
 [Registro de Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
