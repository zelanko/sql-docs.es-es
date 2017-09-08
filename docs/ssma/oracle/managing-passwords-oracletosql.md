---
title: "Administración de contraseñas (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Managing Passwords in Oracle, Exporting or Importing Encrypted Password
- Managing passwords in Oracle, Securing Password
ms.assetid: 8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 14287c0638d066c18662937fa53c41ffc0d4e6cb
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="managing-passwords-oracletosql"></a>Administración de contraseñas (OracleToSQL)
Esta sección es acerca de cómo proteger las contraseñas de la base de datos y el procedimiento para importar o exportar entre servidores:  
  
1.  Protección de contraseña  
  
2.  Exportar o importar la contraseña cifrada  
  
## <a name="securing-password"></a>Protección de contraseña  
SSMA permite proteger la contraseña de una base de datos.  
  
Utilice el procedimiento siguiente para implementar una conexión segura:  
  
Especifique una contraseña válida con uno de los tres métodos siguientes:  
  
1.  **Texto no cifrado:** escriba la contraseña de la base de datos en el atributo value del nodo 'contraseña'. Se encuentra bajo el nodo de definición de servidor en la sección de servidor del archivo de script o el archivo de conexión de servidor.  
  
    Las contraseñas como texto no cifrado no son seguras. Por lo tanto, se producirá el siguiente mensaje de advertencia en la salida de la consola: *"servidor &lt;Id. de servidor&gt; contraseña está siempre en forma no segura como texto no cifrado, aplicación de consola SSMA proporciona una opción para proteger la contraseña a través de cifrado, vea securepassword: opción de archivo de ayuda SSMA para obtener más información."*  
  
    **Las contraseñas cifradas:** la contraseña especificada, en este caso, se almacena en un formato cifrado en el equipo local en ProtectedStorage.ssma.  
  
    -   **Proteger las contraseñas**  
  
        -   Ejecute el `SSMAforOracleConsole.exe` con el `–securepassword` y agregue el modificador de la línea de comandos pasar el servidor de archivos de conexión o el script que contiene el nodo de contraseña en la sección de definición de servidor.  
  
        -   En el símbolo del sistema, el usuario se pide que escriba la contraseña de la base de datos y confírmela.  
  
            Los identificadores de la definición de servidor y sus contraseñas cifradas correspondientes se almacenan en un archivo en el equipo local  
            
            Ejemplo 1:  
            
                Specify password
                
                C:\SSMA\SSMAforOracleConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            Ejemplo 2:
            
                C:\SSMA\SSMAforOracleConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **Quitar contraseñas cifradas**  
  
        Ejecute el `SSMAforOracleConsole.exe` con el`–securepassword` y `–remove` a cambiar en la línea de comandos pasar el Id. de servidor, para quitar las contraseñas cifradas en el archivo de almacenamiento protegido presente en el equipo local.  
        
        Ejemplo:  
        
            C:\SSMA\SSMAforOracleConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforOracleConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **Lista de Id. de servidor cuyas contraseñas están cifradas**  
  
        Ejecute el `SSMAforOracleConsole.exe` con el `–securepassword` y `–list` a cambiar en la línea de comandos para enumerar todos los identificadores de servidor cuyas contraseñas se han cifrado.  
  
        Ejemplo:  
        
            C:\SSMA\SSMAforOracleConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  La contraseña en texto no cifrado mencionado en el archivo de conexión de servidor o la secuencia de comandos tiene prioridad sobre la contraseña cifrada en el archivo protegido.  
    > 2.  Cuando no existe ninguna contraseña en la sección servidor del archivo de conexión de servidor o el archivo de script, o si no ha sido protegido en el equipo local, la consola le pide que escriba la contraseña.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportar o importar las contraseñas cifradas  
La aplicación de consola SSMA permite exportar las contraseñas de cifrado de la base de datos está presente en un archivo en el equipo local a un archivo protegido y viceversa. Ayuda en la creación de la máquina de contraseñas cifradas independientes. Funcionalidad de exportación lee el identificador del servidor y la contraseña de la variable local almacenamiento protegido y guarda la información en un archivo cifrado. Se solicita al usuario que escriba la contraseña para el archivo protegido. Asegúrese de que la contraseña escrita es la longitud de 8 caracteres o más. Este archivo protegido es portátil en distintos equipos. Funcionalidad de importación lee al servidor de la información de identificador y la contraseña desde el archivo protegido. El usuario se le pide que escriba la contraseña para el archivo protegido y anexa la información en el almacenamiento protegido local.  
  
Ejemplo:  

    Export password
    
    Enter password for protecting the exported file C:\SSMA\SSMAforOracleConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforOracleConsole.EXE –p –e "OracleDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
Ejemplo:  

    Import an encrypted password
    
    Enter password for protecting the imported file C:\SSMA\SSMAforOracleConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforOracleConsole.EXE –p –i "OracleDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Vea también  
[Ejecutar la consola SSMA (Oracle)](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  

