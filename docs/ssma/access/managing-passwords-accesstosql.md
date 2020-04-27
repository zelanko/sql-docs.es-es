---
title: Administración de contraseñas (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b099d0f9-dd37-4c87-8b6f-ed0177881ea4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5d8886f28a30f264e0357af82724567e42e3bd5a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907182"
---
# <a name="managing-passwords-accesstosql"></a>Administrar contraseñas (AccessToSQL)
Esta sección trata sobre la protección de contraseñas de base de datos y el procedimiento para importarlas o exportarlas entre servidores:  
  
1.  Protección de contraseñas  
  
2.  Exportar o importar contraseña cifrada  
  
## <a name="securing-password"></a>Protección de contraseñas  
SSMA le permite proteger la contraseña de una base de datos.  
  
Use el procedimiento siguiente para implementar una conexión segura:  
  
Especifique una contraseña válida con uno de los tres métodos siguientes:  
  
1.  **Texto no cifrado:** Escriba la contraseña de la base de datos en el atributo de valor del nodo ' contraseña '. Se encuentra en el nodo definición del servidor en la sección servidor del archivo de script o el archivo de conexión de servidor.  
  
    Las contraseñas en texto no cifrado no son seguras. Por lo tanto, se mostrará el siguiente mensaje de advertencia en la salida de la consola: * &lt;"&gt; la contraseña del ID. del servidor del servidor se proporciona en forma de texto no cifrado no seguro, la aplicación de consola SSMA proporciona una opción para proteger la contraseña a través del cifrado, consulte la opción-securepassword en el archivo de ayuda de SSMA para obtener más información".*  
  
    **Contraseñas cifradas:** La contraseña especificada, en este caso, se almacena en un formato cifrado en el equipo local en ProtectedStorage. SSMA.  
  
    -   **Protección de contraseñas**  
  
        -   Ejecute `SSMAforAccessConsole.exe` con la `-securepassword` línea de comandos y Add switch at pasando la conexión de servidor o el archivo de script que contiene el nodo de contraseña en la sección de definición de servidor.  
  
        -   En el símbolo del sistema, se pide al usuario que escriba la contraseña de la base de datos y la confirme.  
  
            Los identificadores de definición de servidor y sus contraseñas cifradas correspondientes se almacenan en un archivo en el equipo local.  
  
            Ejemplo 1:
            
                Specify password
                
                C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx  
            
            Ejemplo 2:
            
                C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
  
    -   **Quitar contraseñas cifradas**  
  
        Ejecute `SSMAforAccessConsole.exe` con el`-securepassword` modificador `-remove` y en la línea de comandos pasando los identificadores de servidor para quitar las contraseñas cifradas del archivo de almacenamiento protegido presente en el equipo local.  
  
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove all
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove "source_1,target_1"  
  
    -   **Enumerar los identificadores de servidor cuyas contraseñas están cifradas**  
  
        Ejecute el archivo SSMAforAccessConsole. exe con `-securepassword` la `-list` línea de comandos y el modificador at para enumerar todos los identificadores de servidor cuyas contraseñas se han cifrado.  
  
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -list  
  
    > [!NOTE]  
    > 1.  La contraseña en texto no cifrado mencionada en el archivo de conexión de script o servidor tiene prioridad sobre la contraseña cifrada en un archivo protegido.  
    > 2.  Cuando no existe ninguna contraseña en la sección servidor del archivo de conexión del servidor o el archivo de script o si no se ha protegido en el equipo local, la consola de le pide que escriba la contraseña.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportar o importar contraseñas cifradas  
La aplicación de consola SSMA permite exportar contraseñas de base de datos cifradas presentes en un archivo del equipo local a un archivo protegido y viceversa. Ayuda a que las contraseñas cifradas sean independientes de la máquina. La funcionalidad de exportación lee el identificador y la contraseña del servidor desde el almacenamiento protegido local y guarda la información en un archivo cifrado. Se solicita al usuario que escriba la contraseña del archivo protegido. Asegúrese de que la contraseña especificada tiene una longitud de 8 caracteres o más. Este archivo protegido es portátil entre diferentes equipos. La funcionalidad de importación lee el ID. de servidor y la información de contraseña del archivo protegido. Se solicita al usuario que escriba la contraseña del archivo protegido y anexa la información al almacenamiento protegido local.  


    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforAccessConsole.EXE -securepassword -export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE -p -e "AccessDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  


    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforAccessConsole.EXE -securepassword -import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE -p -i "AccessDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Consulte también  
[Ejecutar la consola SSMA (acceso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
