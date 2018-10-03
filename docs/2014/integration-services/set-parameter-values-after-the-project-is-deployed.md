---
title: Establecer valores de parámetro después de implementa el proyecto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5cb12795b0aba94da115916b2b09dc0c2675e8ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151812"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>Establecer valores de parámetro después de la implementación del proyecto
  El Asistente para la implementación permite establecer valores de parámetro predeterminados del servidor al implementar el proyecto en el catálogo. Después de que el proyecto esté en el catálogo, puede utilizar el Explorador de objetos de SQL Server Management Studio (SSMS) o Transact-SQL para establecer valores predeterminados del servidor.  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>Para establecer valores predeterminados del servidor con el Explorador de objetos de SSMS:  
  
1.  Seleccione y haga clic con el botón derecho en el proyecto debajo del nodo **Integration Services**.  
  
2.  Haga clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades del proyecto** .  
  
3.  Abra la página de parámetros haciendo clic en **Parámetros** debajo de **Seleccionar una página**.  
  
4.  Seleccione el parámetro deseado en la lista **Parámetros** . Nota: la columna **Contenedor** ayuda a distinguir los parámetros del proyecto de los parámetros del paquete.  
  
5.  En la columna de **Valor** , especifique el valor del parámetro predeterminado del servidor deseado.  
  
 Para establecer valores predeterminados del servidor con Transact-SQL, use el procedimiento almacenado de [catalog.set_object_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database). Para ver los valores predeterminados actuales del servidor, consulte la vista [catalog.object_parameters &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database). Para borrar un valor predeterminado del servidor, use el procedimiento almacenado [catalog.clear_object_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database).  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; parámetros](integration-services-ssis-package-and-project-parameters.md)  
  
  
