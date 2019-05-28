# Scroll Parallax

A simple Vue Directive to parallax an element. 


### Install

Install the package
`npm install @sil/scroll-parallax`


Import the package

`import ScrollParallax from '~/@sil/scroll-parallax`

Define the component:

```js
	Vue.directive(ScrollParallax);
```

Use the component with default values:

```html
<any-element v-parallax />	
```


#### Arguments

| Argument       | Default     | Description                                                                                           |
| -------------- | ----------- | ----------------------------------------------------------------------------------------------------- |
| debug          | false       | Show debugging information about this element                                                         |
| output         | 'translate' | Options: 'translate' / 'property ', Set the value directly on a translate or on a css custom property |
| originalOffset | 0           | Change the initial offset of the element                                                              |
| minWidth       | 0           | Trigger the parallax from this value.                                                                 |
| amount         | 1.5         | Amount of parallax                                                                                    |
