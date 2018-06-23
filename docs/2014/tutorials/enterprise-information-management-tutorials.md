---
title: Tutoriales de administración de información empresarial | Documentos de Microsoft
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8745dc80-193d-4de0-9f17-ba648ab1e81c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8bf0662a624fac18b83c1bb0d41e4c532d15ad00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107766"
---
# <a name="enterprise-information-management-tutorials"></a>Tutoriales de Administración de información empresarial
  Esta sección contiene tutoriales sobre la administración de información en una empresa mediante las tecnologías de Administración de información empresarial (EIM) incluidas en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Administración de información empresarial (EIM) de la empresa proporciona una cartera de soluciones que permiten a las organizaciones confiar en la credibilidad y la coherencia de sus datos para poder tomar decisiones empresariales críticas. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dispone de las siguientes tecnologías que le ayudan a implementar soluciones de EIM en la empresa.  
  
-   SQL Server Integration Services (SSIS). SSIS proporciona una plataforma extensible y eficaz para la integración de datos procedentes de diversos orígenes en una solución completa de extracción, transformación y carga (ETL) que admite flujos de trabajo empresariales, un almacenamiento de datos o administración de datos maestros.  
  
-   SQL Server Data Quality Services (DQS). DQS permite limpiar, buscar coincidencias, normalizar y enriquecer los datos, de forma que pueda confiar en la información para Business Intelligence, un almacenamiento de datos y cargas de trabajo de procesamiento de transacciones.  
  
-   SQL Server Master Data Services (MDS). MDS proporciona un concentrador central de datos que garantiza que la integridad de la información y la coherencia de los datos son constantes en las distintas aplicaciones.  
  
 [Administración de información empresarial mediante SSIS, MDS y Dqs &#91;Tutorial&#93;](../../2014/tutorials/enterprise-information-management-using-ssis-mds-and-dqs-together-[tutorial].md)  
 En este tutorial, aprenderá a usar conjuntamente SSIS, MDS y DQS para implementar una solución de ejemplo de Administración de información empresaria (EIM). Primero usará DQS para crear una base de conocimiento con los datos de proveedor (metadatos), limpiar los datos de un archivo de Excel según la base de conocimiento, y buscar coincidencias en los datos para identificar y quitar duplicados en los datos. Después usará el complemento MDS para Excel con el fin de cargar los datos limpios y coincidentes en MDS. A continuación, automatizará todo el proceso mediante una solución de SSIS.  
  
## <a name="see-also"></a>Vea también  
 [Administración de información empresarial – Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=270871)  
  
  