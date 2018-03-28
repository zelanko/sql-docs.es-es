---
title: Exportar e importar bases de conocimiento de DQS mediante DQSInstaller.exe | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8060994f8f7da132b848150f1c005140b9eba2c6
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Exportar e importar bases de conocimiento de DQS mediante DQSInstaller.exe
  En el caso de una instalación existente de DQS, puede exportar simultáneamente todas las bases de conocimiento de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] a un archivo de copia de seguridad de DQS (.dqsb) y utilizar después dicho archivo .dqsb para importar simultáneamente todas las bases de conocimiento en otro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] mediante la ejecución del archivo DQSInstaller.exe desde el símbolo del sistema. Para obtener más información acerca de cómo s ejecuta DQSInstaller.exe desde el símbolo del sistema, vea [Run DQSInstaller.exe from Command Prompt](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) en [Run DQSInstaller.exe to Complete Data Quality Server Installation](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
 Esta característica permite realizar una copia de seguridad de *todas* las bases de conocimiento de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] simultáneamente sin necesidad de exportar individualmente cada una de ellas a un archivo .dqs usando [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Asimismo, puede importar *todas* las bases de conocimiento del archivo de copia de seguridad en otro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] simultáneamente sin necesidad de importar individualmente cada una de ellas desde un archivo .dqs usando [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Esto resulta particularmente útil para hacer una copia de seguridad de las bases de conocimiento y restaurarlas durante la desinstalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de un equipo y su posterior instalación en otro. Puede exportar fácilmente todas las bases de conocimiento de una instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] existente a un archivo de copia de seguridad de DQS (.dqsb) y, a continuación, importarlas desde el archivo de copia de seguridad después de haber instalado [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] en otro equipo.  
  
##  <a name="export"></a> Exportar bases de conocimiento a un archivo .dqsb  
 Puede exportar todas las bases de conocimiento de un [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] existente en cualquier momento o al desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].  
  
-   Para exportar todas las bases de conocimiento de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] a un archivo de copia de seguridad de DQS (.dqsb), ejecute DQSInstaller.exe con el parámetro `exportkbs` desde el símbolo del sistema, junto con la ruta de acceso completa y el nombre de archivo donde desea exportar las bases de conocimiento. Por ejemplo, para exportar todas las bases de conocimiento al archivo DQSBackup.dqsb de la unidad C:  
  
    ```  
    dqsinstaller.exe –exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Si el nombre de archivo especificado ya existe en la ubicación especificada, el instalador le preguntará si desea sobrescribir el archivo.  
  
-   Para exportar todas las bases de conocimiento a un archivo de copia de seguridad de DQS mientras desinstala [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], ejecute DQSInstaller.exe con el parámetro `uninstall` desde el símbolo del sistema, junto con la ruta de acceso completa y el nombre de archivo donde desea exportar las bases de conocimiento. Por ejemplo, para exportar todas las bases de conocimiento al archivo DQSBackup.dqsb de la unidad C: y, a continuación, desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]:  
  
    ```  
    dqsinstaller.exe –uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Si no especifica la ruta de acceso completa y el nombre del archivo de copia de seguridad de DQS al desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] desde el símbolo del sistema con el parámetro `uninstall` , se mostrará un mensaje indicando que se eliminarán todas las bases de conocimiento y permitiéndole elegir entre continuar o no con el proceso de desinstalación.  
  
##  <a name="import"></a> Importar bases de conocimiento desde un archivo .dqsb  
 Puede importar todas las bases de conocimiento desde un archivo de copia de seguridad de DQS (.dqsb) después de completar la instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Para importar bases de conocimiento, debe tener un archivo de copia de seguridad de DQS (.dqsb) válido.  
  
 Ejecute el archivo DQSInstaller.exe con el parámetro `importkbs` desde el símbolo del sistema, junto con la ruta de acceso completa y el nombre de archivo del que desea importar las bases de conocimiento. Por ejemplo, para importar todas las bases de conocimiento desde el archivo DQSBackup.dqsb de la unidad C:  
  
```  
dqsinstaller.exe –importkbs c:\DQSBackup.dqsb  
```  
  
 Si ya existen bases de conocimiento en [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] que tienen el mismo nombre que las que va a importar, a los nombres de las bases de datos importadas se les agregará un carácter de subrayado (_) seguido de un valor entero, comenzando por 1. Por ejemplo, si el dominio “CompanyName” está duplicado, el nombre del dominio importado será “CompanyName_1”.  
  
## <a name="see-also"></a>Ver también  
 [Ejecutar DQSInstaller.exe para completar la instalación del servidor de calidad de datos](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Instalar Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Exportar una base de conocimiento a un archivo .dqs](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [Importar una base de conocimiento desde un archivo .dqs](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
