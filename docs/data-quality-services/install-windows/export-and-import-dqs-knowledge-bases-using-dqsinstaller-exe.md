---
title: Exportar e importar bases de conocimiento de DQS mediante DQSInstaller. exe
description: Aprenda a usar DQSInstaller. exe para exportar e importar bases de conocimiento de DQS para SQL Server Data Quality Services (DQS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ae87b9daebdef6b81c4d96abc253820cf7cb8228
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75558157"
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Exportar e importar bases de conocimiento de DQS mediante DQSInstaller.exe

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En el caso de una instalación existente de DQS, puede exportar simultáneamente todas las bases de conocimiento de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] a un archivo de copia de seguridad de DQS (.dqsb) y utilizar después dicho archivo .dqsb para importar simultáneamente todas las bases de conocimiento en otro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] mediante la ejecución del archivo DQSInstaller.exe desde el símbolo del sistema. Para obtener más información acerca de cómo s ejecuta DQSInstaller.exe desde el símbolo del sistema, vea [Ejecutar DQSInstaller.exe desde el símbolo del sistema](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) en [Ejecutar DQSInstaller.exe para completar la instalación del servidor de calidad de datos](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
 Esta característica permite realizar una copia de seguridad de *todas* las bases de conocimiento de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] simultáneamente sin necesidad de exportar individualmente cada una de ellas a un archivo .dqs usando [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Asimismo, puede importar *todas* las bases de conocimiento del archivo de copia de seguridad en otro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] simultáneamente sin necesidad de importar individualmente cada una de ellas desde un archivo .dqs usando [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Esto resulta particularmente útil para hacer una copia de seguridad de las bases de conocimiento y restaurarlas durante la desinstalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de un equipo y su posterior instalación en otro. Puede exportar fácilmente todas las bases de conocimiento de una instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] existente a un archivo de copia de seguridad de DQS (.dqsb) y, a continuación, importarlas desde el archivo de copia de seguridad después de haber instalado [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] en otro equipo.  
  
##  <a name="export"></a>Exportar bases de conocimiento a un archivo. dqsb  
 Puede exportar todas las bases de conocimiento de un [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] existente en cualquier momento o al desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].  
  
-   Para exportar todas las bases de conocimiento de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] a un archivo de copia de seguridad de DQS (.dqsb), ejecute DQSInstaller.exe con el parámetro `exportkbs` desde el símbolo del sistema, junto con la ruta de acceso completa y el nombre de archivo donde desea exportar las bases de conocimiento. Por ejemplo, para exportar todas las bases de conocimiento al archivo DQSBackup.dqsb de la unidad C:  
  
    ```  
    dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Si el nombre de archivo especificado ya existe en la ubicación especificada, el instalador le preguntará si desea sobrescribir el archivo.  
  
-   Para exportar todas las bases de conocimiento a un archivo de copia de seguridad de DQS mientras desinstala [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], ejecute DQSInstaller.exe con el parámetro `uninstall` desde el símbolo del sistema, junto con la ruta de acceso completa y el nombre de archivo donde desea exportar las bases de conocimiento. Por ejemplo, para exportar todas las bases de conocimiento al archivo DQSBackup.dqsb de la unidad C: y, a continuación, desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]:  
  
    ```  
    dqsinstaller.exe -uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Si no especifica la ruta de acceso completa y el nombre del archivo de copia de seguridad de DQS al desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] desde el símbolo del sistema con el parámetro `uninstall` , se mostrará un mensaje indicando que se eliminarán todas las bases de conocimiento y permitiéndole elegir entre continuar o no con el proceso de desinstalación.  
  
##  <a name="import"></a>Importar bases de conocimiento desde un archivo. dqsb  
 Puede importar todas las bases de conocimiento desde un archivo de copia de seguridad de DQS (.dqsb) después de completar la instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Para importar bases de conocimiento, debe tener un archivo de copia de seguridad de DQS (.dqsb) válido.  
  
 Ejecute el archivo DQSInstaller.exe con el parámetro `importkbs` desde el símbolo del sistema, junto con la ruta de acceso completa y el nombre de archivo del que desea importar las bases de conocimiento. Por ejemplo, para importar todas las bases de conocimiento desde el archivo DQSBackup.dqsb de la unidad C:  
  
```  
dqsinstaller.exe -importkbs c:\DQSBackup.dqsb  
```  
  
 Si ya existen bases de conocimiento en [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] que tienen el mismo nombre que las que va a importar, a los nombres de las bases de datos importadas se les agregará un carácter de subrayado (_) seguido de un valor entero, comenzando por 1. Por ejemplo, si el dominio "CompanyName" está duplicado, el nombre del dominio importado será "CompanyName_1".  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar DQSInstaller. exe para completar la instalación del servidor de calidad de datos](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Instalar Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Exportar una base de conocimiento a un archivo. DQS](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [Importar una base de conocimiento desde un archivo .dqs](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
