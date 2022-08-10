---
title: Web Components
slug: Web/Web_Components
tags:
  - Landing
  - Web Components
translation_of: Web/Web_Components
---
<div>{{DefaultAPISidebar("Web Components")}}</div>

<p>Web Components 是一套不同的技术，允许您创建可重用的定制元素（它们的功能封装在您的代码之外）并且在您的 web 应用中使用它们。</p>

<h2 id="概念和使用">概念和使用</h2>

<p>作为开发者，我们都知道尽可能多的重用代码是一个好主意。这对于自定义标记结构来说通常不是那么容易 — 想想复杂的 HTML（以及相关的样式和脚本），有时您不得不写代码来呈现自定义 UI 控件，并且如果您不小心的话，多次使用它们会使您的页面变得一团糟。</p>

<p>Web Components 旨在解决这些问题 — 它由三项主要技术组成，它们可以一起使用来创建封装功能的定制元素，可以在你喜欢的任何地方重用，不必担心代码冲突。</p>

<ul>
 <li><strong>Custom elements（自定义元素）：</strong>一组 JavaScript API，允许您定义 custom elements 及其行为，然后可以在您的用户界面中按照需要使用它们。</li>
 <li><strong>Shadow DOM（影子 DOM）</strong>：一组 JavaScript API，用于将封装的“影子”DOM 树附加到元素（与主文档 DOM 分开呈现）并控制其关联的功能。通过这种方式，您可以保持元素的功能私有，这样它们就可以被脚本化和样式化，而不用担心与文档的其他部分发生冲突。</li>
 <li><strong>HTML templates（HTML 模板）：</strong> {{HTMLElement("template")}} 和 {{HTMLElement("slot")}} 元素使您可以编写不在呈现页面中显示的标记模板。然后它们可以作为自定义元素结构的基础被多次重用。</li>
</ul>

<p>实现 web component 的基本方法通常如下所示：</p>

<ol>
 <li>创建一个类或函数来指定 web 组件的功能，如果使用类，请使用 ECMAScript 2015 的类语法 (参阅<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes">类</a>获取更多信息)。</li>
 <li>使用 {{domxref("CustomElementRegistry.define()")}} 方法注册您的新自定义元素 ，并向其传递要定义的元素名称、指定元素功能的类、以及可选的其所继承自的元素。</li>
 <li>如果需要的话，使用{{domxref("Element.attachShadow()")}} 方法将一个 shadow DOM 附加到自定义元素上。使用通常的 DOM 方法向 shadow DOM 中添加子元素、事件监听器等等。</li>
 <li>如果需要的话，使用 {{htmlelement("template")}} 和{{htmlelement("slot")}} 定义一个 HTML 模板。再次使用常规 DOM 方法克隆模板并将其附加到您的 shadow DOM 中。</li>
 <li>在页面任何您喜欢的位置使用自定义元素，就像使用常规 HTML 元素那样。</li>
</ol>

<h2 id="教程">教程</h2>

<dl>
 <dt><a href="/zh-CN/docs/Web/Web_Components/Using_custom_elements">Using custom elements</a></dt>
 <dd>介绍如何使用自定义元素的功能来创建简单的 web components，以及生命周期回调和其他更高级的功能。</dd>
 <dt><a href="/zh-CN/docs/Web/Web_Components/Using_shadow_DOM">Using shadow DOM</a></dt>
 <dd>介绍 shadow DOM 的基础知识，展示如何向元素中附加 shadow DOM，添加到 shadow DOM 树，添加样式等等。</dd>
 <dt><a href="/zh-CN/docs/Web/Web_Components/Using_templates_and_slots">Using templates and slots</a></dt>
 <dd>介绍如何使用{{htmlelement("template")}} 和 {{htmlelement("slot")}} 元素定义可重用的 HTML 结构，然后在 Web components 中使用该结构。</dd>
</dl>

<h2 id="参考">参考</h2>

<h3 id="Custom_elements">Custom elements</h3>

<dl>
 <dt>{{domxref("CustomElementRegistry")}}</dt>
 <dd>包含自定义元素相关功能，最值得注意的是 {{domxref("CustomElementRegistry.define()")}} 方法用来注册新的自定义元素，这样就可以在文档中使用它们。</dd>
 <dt>{{domxref("Window.customElements")}}</dt>
 <dd>返回 <code>CustomElementRegistry</code> 对象的引用。</dd>
 <dt><a href="/zh-CN/docs/Web/Web_Components/Using_custom_elements#Using_the_lifecycle_callbacks">生命周期回调</a></dt>
 <dd>定义在自定义元素的类定义中的特殊回调函数，影响其行为：
 <ul>
  <li><code>connectedCallback</code>: 当自定义元素第一次被连接到文档 DOM 时被调用。</li>
  <li><code>disconnectedCallback</code>: 当自定义元素与文档 DOM 断开连接时被调用。</li>
  <li><code>adoptedCallback</code>: 当自定义元素被移动到新文档时被调用。</li>
  <li><code>attributeChangedCallback</code>: 当自定义元素的一个属性被增加、移除或更改时被调用。</li>
 </ul>
 </dd>
</dl>

<dl>
 <dt>创建自定义内置元素的扩展</dt>
 <dd>定义了以下扩展：
 <ul>
  <li>{{htmlattrxref("is")}} 全局 HTML 属性：允许您指定一个标准 HTML 元素应该表现得像一个已注册的自定义内置元素。</li>
  <li>{{domxref("Document.createElement()")}} 方法的“is”选项：允许您创建一个标准 HTML 元素的实例，表现得像一个给定的已注册的自定义内置元素。</li>
 </ul>
 </dd>
 <dt>CSS 伪类</dt>
 <dd>与自定义元素特别相关的伪类：
 <ul>
  <li>{{cssxref(":defined")}}: 匹配任何已定义的元素，包括内置元素和使用<code>CustomElementRegistry.define()</code>定义的自定义元素。</li>
  <li>{{cssxref(":host")}}: 选择 <a href="/en-US/docs/Web/Web_Components/Using_shadow_DOM">shadow DOM </a>的 shadow host ，内容是它内部使用的 CSS（ containing the CSS it is used inside ）。</li>
  <li>{{cssxref(":host()")}}: 选择 <a href="/en-US/docs/Web/Web_Components/Using_shadow_DOM">shadow DOM </a>的 shadow host ，内容是它内部使用的 CSS（这样您可以从 shadow DOM 内部选择自定义元素）— 但只匹配给定方法的选择器的 shadow host 元素。</li>
  <li>{{cssxref(":host-context", ":host-context()")}}: 选择 <a href="/en-US/docs/Web/Web_Components/Using_shadow_DOM">shadow DOM </a>的 shadow host ，内容是它内部使用的 CSS（这样您可以从 shadow DOM 内部选择自定义元素）— 但只匹配给定方法的选择器匹配元素的子 shadow host 元素。</li>
 </ul>
 </dd>
</dl>

<h3 id="Shadow_DOM">Shadow DOM</h3>

<dl>
 <dt>{{domxref("ShadowRoot")}}</dt>
 <dd>表示 shadow DOM 子树的根节点。</dd>
 <dt>{{domxref("DocumentOrShadowRoot")}}</dt>
 <dd>定义了可在文档和 shadow 根中使用的功能的 mixin。</dd>
 <dt>{{domxref("Element")}} extensions</dt>
 <dd>与 shadow DOM 有关的<code>Element</code> 接口的扩展：
 <ul>
  <li>{{domxref("Element.attachShadow()")}} 方法将 shadow DOM 树附加给特定元素。</li>
  <li>{{domxref("Element.shadowRoot")}} 属性返回附加给特定元素的 shadow root，或者 <code>null</code> 如果没有 shadow root 被附加。</li>
 </ul>
 </dd>
 <dt>{{domxref("Node")}} 相关拓展</dt>
 <dd>与 shadow DOM 相关的 <code>Node</code> 接口的拓展：
 <ul>
  <li>{{domxref("Node.getRootNode()")}} 方法返回上下文对象的根，可以选择包含 shadow root，如果可用的话。</li>
  <li>{{domxref("Node.isConnected")}} 属性返回一个布尔值表示节点是否连接（直接或间接）到上下文对象。例如，在普通 DOM 的情况下为{{domxref("Document")}} 对象，或者在 shadow DOM 的情况下为 {{domxref("ShadowRoot")}} 。</li>
 </ul>
 </dd>
 <dt>{{domxref("Event")}} 拓展</dt>
 <dd>与 shadow DOM 相关的 <code>Event</code> 接口的扩展：
 <ul>
  <li>{{domxref("Event.composed")}}: 返回 {{jsxref("Boolean")}} 它表明事件是否会通过 shadow DOM 边界传播到标准 DOM。</li>
  <li>返回事件的路径（侦听器将被调用的对象）。如果 shadow root 是使用{{domxref("ShadowRoot.mode")}}为 closed 创建的，则不包括 shadow 树中的节点。</li>
 </ul>
 </dd>
</dl>

<h3 id="HTML_templates">HTML templates</h3>

<dl>
 <dt>{{htmlelement("template")}}</dt>
 <dd>包含一个 HTML 片段，不会在文档初始化时渲染。但是可以在运行时使用 JavaScript 显示。主要用作自定义元素结构的基础。关联的 DOM 接口是{{domxref("HTMLTemplateElement")}}。</dd>
 <dt>{{htmlelement("slot")}}</dt>
 <dd>web component 中的一个占位符，你可以填充自己的标记，这样你就可以创建单独的 DOM 树并将它们呈现在一起。关联的 DOM 接口是{{domxref("HTMLSlotElement")}}。</dd>
 <dt>The <code><a href="/en-US/docs/Web/HTML/Global_attributes/slot">slot</a></code> global HTML attribute</dt>
 <dd>将在 shadow DOM 树中的插槽分配给一个元素。</dd>
 <dt>{{domxref("Slotable")}}</dt>
 <dd>由 {{domxref("Element")}} 和 {{domxref("Text")}} 节点实现的 mixin，定义了允许它们成为 {{htmlelement("slot")}} 元素内容的特性。mixin 定义了一个属性， {{domxref("Slotable.assignedSlot")}}，返回节点所插入的插槽的引用。</dd>
</dl>

<dl>
 <dt>{{domxref("Element")}} extensions</dt>
 <dd>与插槽相关的 <code>Element</code> 接口的扩展：
 <ul>
  <li>{{domxref("Element.slot")}}：返回附加到元素上的 shadow DOM 插槽的名字。</li>
 </ul>
 </dd>
 <dt>CSS pseudo-elements</dt>
 <dd>slots 特别相关的伪元素：
 <ul>
  <li>{{cssxref("::slotted")}}：匹配任何已经插入一个 slot 的内容。</li>
 </ul>
 </dd>
 <dt>The {{event("slotchange")}} event</dt>
 <dd>当插槽中的节点改变时在 {{domxref("HTMLSlotElement")}} 实例（<a href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/slot"><code>&lt;slot&gt;</code></a> 元素）上触发。</dd>
</dl>

<h2 id="例子">例子</h2>

<p>在 <a href="https://github.com/mdn/web-components-examples">web-components-examples</a>，我们正在构建一些例子。以后会添加更多。</p>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat}}

<h2 id="另见">另见</h2>

<ul>
 <li><a href="https://www.webcomponents.org/">webcomponents.org</a> — site featuring web components examples, tutorials, and other information.</li>
 <li><a href="https://github.com/hybridsjs/hybrids">Hybrids</a> — Open source web components library, which favors plain objects and pure functions over <code>class</code> and this syntax. It provides a simple and functional API for creating custom elements.</li>
 <li><a href="https://www.polymer-project.org/">Polymer</a> — Google's web components framework — a set of polyfills, enhancements, and examples. Currently the easiest way to use web components cross-browser.</li>
 <li><a href="https://github.com/devpunks/snuggsi#readme">Snuggsi.es</a> — Easy Web Components in ~1kB <em>Including polyfill</em> — All you need is a browser and basic understanding of HTML, CSS, and JavaScript classes to be productive.</li>
 <li><a href="https://github.com/slimjs/slim.js">Slim.js</a> — Open source web components library — a high-performant library for rapid and easy component authoring; extensible and pluggable and cross-framework compatible.</li>
 <li><a href="https://www.htmlelements.com/">Smart.js</a> — Web Components library with simple API for creating cross-browser custom elements.</li>
 <li><a href="https://stenciljs.com/">Stencil</a> — Toolchain for building reusable, scalable design systems in web components.</li>
</ul>