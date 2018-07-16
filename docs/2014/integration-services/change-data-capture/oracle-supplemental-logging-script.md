---
title: Script de registro complementario de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5e6ee618-b89b-46c7-92ad-4fc5ef7b777a
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c982204b6d8bbb5140a612388028db0fb0e194e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274981"
---
# <a name="oracle-supplemental-logging-script"></a>Script de registro complementario de Oracle
  Este cuadro de diálogo muestra el script de registro complementario de Oracle.  
  
 Al preparar una instancia CDC para su uso, el diseñador CDC crea un script SQL de Oracle que configura el registro complementario para las tablas que se van a capturar. El script de registro complementario indica a Oracle que cuando se actualiza una tabla determinada, los registros de cambios que escribe en el registro de transacciones deben contener los datos de todas las columnas de interés, no solo de las columnas que han cambiado.  
  
 Dependiendo de las directivas DBA de Oracle de la organización, la ejecución del script de registro complementario puede necesitar su revisión y aprobación por parte de un administrador de bases de datos de Oracle.  
  
## <a name="options"></a>Opciones  
 A continuación se indican las opciones disponibles sobre cómo ejecutar el script.  
  
 **Ejecutar script**  
 Ejecuta el script de registro complementario en las tablas definidas para la instancia CDC. Para ejecutar este script, el usuario de Oracle debe tener el permiso ALTER TABLE para todas las tablas que se van a capturar y el permiso SELECT en la vista DBA_LOG_GROUPS. Además, el usuario de Oracle debe tener las credenciales para usar una base de datos de Oracle con los permisos necesarios. Puede permitir que el programa le solicite las credenciales de Oracle y que ejecute el script.  
  
 **Guardar como**  
 Guarda el script en un archivo de texto. Se emplea si un administrador de bases de datos (DBA) de Oracle necesita examinar y ejecutar el script de registro complementario; el programa le permite guardar el script en un archivo de texto que puede enviar posteriormente al DBA de Oracle por correo electrónico o por otros medios para su ejecución posterior (mediante la utilidad SQL*Plus de Oracle u otra herramienta para ejecutar scripts en una base de datos de Oracle).  
  
 **Copiar**  
 Copia el script en el Portapapeles. Cuando esté listo, puede pegar el script en cualquier ubicación que desee por si un administrador de bases de datos (DBA) de Oracle necesita examinar y ejecutar el script de registro complementario.  
  
## <a name="see-also"></a>Vea también  
 [Cómo administrar una instancia CDC](manage-a-cdc-instance.md)   
 [Administrar una instancia CDC](manage-a-cdc-instance.md)  
  
  
