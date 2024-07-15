```js
import * as vscode from 'vscode';

// 获取当前激活的文档
const activeEditor = vscode.window.activeTextEditor;
if (activeEditor) {
    // 获取当前文档对象
    const document = activeEditor.document;

    // 获取文档内容
    const content = document.getText();

    // 修改文档内容
    const newContent = content.replace('old text', 'new text');

    // 将修改后的内容应用到文档
    const edit = new vscode.WorkspaceEdit();
    edit.replace(
        document.uri,
        new vscode.Range(
            document.positionAt(0),
            document.positionAt(content.length)
        ),
        newContent
    );

    // 应用编辑
    vscode.workspace.applyEdit(edit);
}
```

在这个示例中，我们首先获取当前激活的文档，并获取其内容。然后，我们根据需求修改文档内容，并创建一个 WorkspaceEdit 对象来表示编辑。接着，我们通过 replace 方法来指定要替换的范围和新的内容。最后，我们调用 applyEdit 方法来应用编辑，即修改了文档的内容。

请根据你的实际需求调整代码，并确保在调用 applyEdit 方法时传递了正确的编辑对象，以确保成功修改文件内容。

```js
import * as vscode from 'vscode';

export function activate(context: vscode.ExtensionContext) {
    let disposable = vscode.commands.registerCommand('extension.insertBelowCursor', () => {
        // 获取当前激活的文档编辑器
        const editor = vscode.window.activeTextEditor;
        if (editor) {
            // 获取光标位置
            const position = editor.selection.active;
            // 获取下一行的行号
            const nextLineNumber = position.line + 1;
            // 构造插入内容
            const insertion = '\n// Inserted text';
            // 插入文本
            editor.edit((editBuilder) => {
                // 在下一行插入内容
                editBuilder.insert(new vscode.Position(nextLineNumber, 0), insertion);
            });
        }
    });

    context.subscriptions.push(disposable);
}
```

在这个示例中，我们注册了一个命令 extension.insertBelowCursor，当该命令被执行时，会在光标的下一行添加指定的内容。首先，我们获取当前激活的文档编辑器，并获取光标的位置信息。然后，我们计算出下一行的行号，并构造需要插入的内容。最后，我们使用 editBuilder.insert() 方法在下一行插入内容。
