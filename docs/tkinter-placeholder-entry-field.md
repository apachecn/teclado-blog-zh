# 如何将占位符添加到 Tkinter 输入字段

> 原文：<https://blog.teclado.com/tkinter-placeholder-entry-field/>

原生 Tkinter `Entry`小部件不支持占位符——当字段为空时出现的文本，当字段不为空时消失。

在这篇博文中，我们将尝试在自定义 Tkinter 小部件中添加这一功能，并向您展示我们是如何做到的！

这篇博文的想法来自我们课程中一个学生的问题，用 Python 和 Tkinter 开发 GUI。如果您想了解更多关于 Tkinter 和 GUI 开发的知识，请查看课程！

## 占位符里有什么？

在 Tkinter 中开始实现占位符的最好方法是从用户交互的角度考虑占位符的行为方式。当我们这样做时，我们将能够把这种行为转换成可以绑定到小部件的事件。

通常 Tkinter 占位符是这样实现的:

*   如果用户没有键入任何内容，占位符文本会在字段失去焦点时出现
*   当字段获得焦点时(但在用户键入之前)，占位符文本会消失

HTML 占位符的行为稍有不同，但是它们的行为更难用 Tkinter 复制，所以我们将坚持使用这个实现！

## 创建自定义入口小部件

要创建自定义小部件，我们要做的是编写一个类，并使它从目标小部件继承。然后，在该类中，我们可以根据需要对小部件进行更改。

让我们从在一个新类中继承`ttk.Entry`开始:

```py
from tkinter import ttk

class PlaceholderEntry(ttk.Entry):
    def __init__(self, container, *args, **kwargs):
        super().__init__(container, *args, **kwargs) 
```

这段代码的意思是，无论何时创建一个`PlaceholderEntry`对象，它与创建一个`ttk.Entry`对象是一样的。现在让我们扩展它，使字段以一些文本开始。我们将:

*   向`__init__`方法添加一个必需的`placeholder`参数。
*   在小部件中插入文本。

让我们来看看如何做到这一点:

```py
from tkinter import ttk

class PlaceholderEntry(ttk.Entry):
    def __init__(self, container, placeholder, *args, **kwargs):
        super().__init__(container, *args, **kwargs)

        self.insert("1.0", placeholder) 
```

接下来，我们将使文本获得焦点时，内容被删除。

## 添加事件绑定

为了在文本获得焦点时删除内容，我们将向该字段添加一个事件绑定。函数可以绑定在特定的事件上，如`<KeyPressed>`、`<FocusIn>`或`<FocusOut>`。我们将利用后两种方法来实现:

```py
from tkinter import ttk

class PlaceholderEntry(ttk.Entry):
    def __init__(self, container, placeholder, *args, **kwargs):
        super().__init__(container, *args, **kwargs)

		self.insert("0", placeholder)
		self.bind("<FocusIn>", self._clear_placeholder)

	def _clear_placeholder(self, e):
		self.delete("0", "end") 
```

接下来，让我们这样做，当字段失去焦点时，占位符被添加回来(只要字段中还没有文本)。

```py
from tkinter import ttk

class PlaceholderEntry(ttk.Entry):
    def __init__(self, container, placeholder, *args, **kwargs):
        super().__init__(container, *args, **kwargs)
		self.placeholder = placeholder

		self.insert("0", self.placeholder)
		self.bind("<FocusIn>", self._clear_placeholder)
		self.bind("<FocusOut>", self._add_placeholder)

	def _clear_placeholder(self, e):
		self.delete("0", "end")

	def _add_placeholder(self, e):
		if not self.get():
            self.insert("0", self.placeholder) 
```

目前我们有几个 bug:

*   如果用户在字段中键入一些内容，然后单击离开，将焦点放回字段将删除他们键入的所有内容。
*   占位符看起来像是已经输入到字段中的文本，所以可能会有点混乱！

让我们一次性解决这两个问题。

## 更改占位符的文本颜色

Tkinter 字段有背景色(文本框的颜色)和前景色(文本的颜色)。为了改变占位符的颜色，我们必须在每次占位符出现时改变前景色；并在占位符消失时将它改回来，以便用户的文本保持正常颜色。

为此，我们将为带有占位符的输入字段定义一种样式(带有浅灰色前景色)。我们将把这个样式设置为这个入口类的默认样式。

每当我们清除占位符时，我们会将样式重置回默认值`"TEntry"`。在这里，我们也可以这样做，这样每当字段失去焦点时，我们也不会删除用户的内容:

```py
import tkinter as tk
from tkinter import ttk

class PlaceholderEntry(ttk.Entry):
    def __init__(self, container, placeholder, *args, **kwargs):
        super().__init__(container, *args, style="Placeholder.TEntry", **kwargs)
		self.placeholder = placeholder

		self.insert("0", self.placeholder)
		self.bind("<FocusIn>", self._clear_placeholder)
		self.bind("<FocusOut>", self._add_placeholder)

	def _clear_placeholder(self, e):
		if self["style"] == "Placeholder.TEntry":
			self.delete("0", "end")
			self["style"] = "TEntry"

	def _add_placeholder(self, e):
		if not self.get():
			self.insert("0", self.placeholder)
			self["style"] = "Placeholder.TEntry"

root = tk.Tk()
style = ttk.Style(root)

style.configure("Placeholder.TEntry", foreground="#d5d5d5")

entry = PlaceholderEntry(root, "Sample placeholder")
entry.pack()

root.mainloop() 
```

## 允许自定义占位符样式

自定义输入字段类的用户可能不希望每次都使用`"Placeholder.TEntry"`样式。他们可能想给它起个不同的名字，这样他们就可以用他们自己的名字了。

当您创建要在多个地方使用的自定义小部件时，您应该避免使用硬编码的样式和设置。相反，您可以做的是允许传递关键字参数。如果你认为合适的话，你也可以使用合理的默认值。

请记住，如果我们的字段试图使用`"Placeholder.TEntry"`，但是用户之前没有定义，我们将会崩溃并出现错误。

```py
class PlaceholderEntry(ttk.Entry):
    def __init__(self, container, placeholder, *args, **kwargs):
        super().__init__(container, *args, **kwargs)
		self.placeholder = placeholder

		self.field_style = kwargs.pop("style", "TEntry")
		self.placeholder_style = kwargs.pop("placeholder_style", self.field_style)
		self["style"] = self.placeholder_style

		self.insert("0", self.placeholder)
		self.bind("<FocusIn>", self._clear_placeholder)
		self.bind("<FocusOut>", self._add_placeholder)

	def _clear_placeholder(self, e):
		if self["style"] == self.placeholder_style:
			self.delete("0", "end")
			self["style"] = self.field_style

	def _add_placeholder(self, e):
		if not self.get():
			self.insert("0", self.placeholder)
			self["style"] = self.placeholder_style 
```

有了这些改变，现在我们可以像这样创建`PlaceholderEntry`小部件:

```py
entry = PlaceholderEntry(
    root,
	"Sample Placeholder",
	style="TEntry",
	placeholder_style="Placeholder.TEntry"
) 
```

如果您没有通过`style`或`placeholder_style`，默认的`"TEntry"`将用于这两者。如果你只传递了`style`，那么`placeholder_style`也会接受它的值，所以这个字段看起来总是一样的。

## 包扎

我们已经学习了如何创建自定义小部件，以及如何将占位符文本添加到输入字段。请随意使用`PlaceholderEntry`类，并在您自己的项目中重用它！

我希望这是有用的。如果是的话，如果你想学习更多关于使用 Python 开发 Tkinter 和 GUI 的知识，请查看我们的课程:[使用 Python 和 Tkinter 开发 GUI](https://www.udemy.com/course/desktop-gui-python-tkinter/?referralCode=8A984196616D9BF14DD0)。我们很希望你能加入我们的课程。

感谢您的阅读，我们下次再见！