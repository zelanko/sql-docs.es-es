---
title: "Agregar fragmentos de código de Transact-SQL| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: be592feef35a8cf875d9dce783f5843979d4f835
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="add-transact-sql-snippets"></a>Agregar fragmentos de código de Transact-SQL
  Puede agregar sus propios fragmentos de código de Transact-SQL al conjunto de fragmentos de código predefinidos que se incluyen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="creating-a-transact-sql-snippet-file"></a>Crear un archivo de fragmento de código de Transact-SQL  
 La primera parte de la creación de un fragmento de código de [!INCLUDE[tsql](../../includes/tsql-md.md)] consiste en crear un archivo XML con el texto del fragmento de código. El archivo debe tener una extensión de archivo .snippet y cumplir los requisitos del tema sobre [referencia de esquemas de fragmento de código](http://go.microsoft.com/fwlink/?LinkId=207504). El lenguaje del fragmento de código se establece en SQL.  
  
 Puede utilizar los fragmentos de código predefinidos que se proporcionan con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como ejemplos. Para buscar los fragmentos de código predefinidos, abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione el menú **Herramientas** y haga clic en **Administrador de fragmentos de código**. Seleccione **SQL** en el cuadro de lista **Lenguaje** ; la ruta de acceso a los fragmentos de código de [!INCLUDE[tsql](../../includes/tsql-md.md)] se muestra en el cuadro **Ubicación** .  
  
## <a name="registering-the-code-snippet"></a>Registrar el fragmento de código  
 Después de crear el archivo de fragmento de código, utilice el Administrador de fragmentos de código para registrar el fragmento de código con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Puede agregar una carpeta que contiene varios fragmentos de código o importar fragmentos de código individuales a la carpeta **Mis fragmentos de código** .  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="adding-a-snippet-folder"></a>Agregar una carpeta de fragmentos de código  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Seleccione el menú **Herramientas** y haga clic en **Administrador de fragmentos de código**.  
  
3.  Haga clic en el botón **Agregar** .  
  
4.  Navegue a la carpeta que contiene los fragmentos de código y haga clic en el botón **Seleccionar carpeta** .  
  
#### <a name="importing-a-snippet"></a>Importar un fragmento de código  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Seleccione el menú **Herramientas** y haga clic en **Administrador de fragmentos de código**.  
  
3.  Haga clic en el botón **Importar** .  
  
4.  Navegue a la carpeta que contiene el fragmento de código, haga clic en el archivo .snippet y haga clic en el botón **Abrir** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un fragmento de código rodear con **TRY-CATCH** y se importa a [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  Pegue el código siguiente en el Bloc de notas y, a continuación, guárdelo como un archivo denominado TryCatch.snippet.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
3.  Seleccione el menú **Herramientas** y haga clic en **Administrador de fragmentos de código**.  
  
4.  Haga clic en el botón **Importar** .  
  
5.  Navegue a la carpeta que contiene el archivo TryCatch.snippet, haga clic en el citado archivo y haga clic en el botón **Abrir** . No debe haber un fragmento de código TryCatch en la carpeta **Mis fragmentos de código** .  
  
## <a name="see-also"></a>Vea también  
 [Insertar fragmentos de código de Transact-SQL para rodear](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
