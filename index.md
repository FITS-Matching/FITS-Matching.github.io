---
layout: default
---

<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>MathJax example</title>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async
            src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
    </script>
  </head>
  <body>
    <p>
      For images polluted by software noise, the extracted noise residual \(\widehat{\mathbf{K}}\) can be expressed as the sum of three components:
    </p>
    <p>
      \[\widehat{\mathbf{K}} = \alpha \mathbf{K} + \beta \mathbf{S} + \mathbf{\xi},\]
    </p>
    <p>
      where \(\mathbf{K}\), \(\mathbf{S}\), and \(\mathbf{\xi}\) are hardware fingerprint, software noise, and other types of noise sources respectively. A fingerprint extracting algorithm cannot completely extract the fingerprints. Therefore, we add coefficients \(\alpha\) and \(\beta\) before \(\mathbf{K}\) and \(\mathbf{S}\) respectively.
    </p>
    <p>
      Please note that for the dot product of two matrices: \(\mathbf{X} \odot \mathbf{Y} = \sum_{i=1}^{m}\sum_{j=1}^{n} \mathbf{X}[i,j] \mathbf{Y}[i,j]\). If \(\mathbf{X}\) isn't correlative with \(\mathbf{Y}\), the result behaves as random noise. Since the mean of random noise is statistically close to zero, it can be ignored.
    </p>
  </body>
</html>

## 1.Detailed explanation of FITS_CC

<html>
  <body>
    <p>
      According to Equation (\ref{eq:CC}), for a pair of estimated fingerprints \(\widehat{\mathbf{K}}_Q\) and \(\widehat{\mathbf{K}}_R\), the cross correlation (CC) between them can be expressed as follows,
    </p>
    <p>
      \[\operatorname{CC}(\widehat{\mathbf{K}}_Q, \widehat{\mathbf{K}}_R) = (\alpha_Q \mathbf{K}_{Qm} + \beta_Q \mathbf{S}_{Qm} + \xi_{Qm}) \odot (\alpha_R \mathbf{K}_{Rm} + \beta_R \mathbf{S}_{Rm} + \xi_{Rm})\]
    </p>
    <p>
      \[= \alpha_Q \alpha_R \mathbf{K}_{Qm} \odot \mathbf{K}_{Rm} + \beta_{Q}\beta_{R} \mathbf{S}_{Qm} \odot \mathbf{S}_{Rm} + \mathbf{\varphi}_{QR},\]
    </p>
    <p>
      where \(\varphi_{QR}\) is a combination of multiple random noises. Specifically,
    </p>
    <p>
      \[\varphi_{QR} = \alpha_Q \beta_R \mathbf{K}_{Qm} \odot \mathbf{S}_{Rm}
            + \alpha_Q \mathbf{K}_{Qm} \odot \xi_{Rm} 
            + \beta_{Q} \alpha_{R} \mathbf{S}_{Qm} \odot \mathbf{K}_{Rm}\\
            + \beta_Q \mathbf{S}_{Q_m}\odot \xi_{Rm}
            + \alpha_R \xi_{Qm} \odot \mathbf{K}_{Rm}
            + \beta_R \xi_{Qm} \odot \mathbf{S}_{Rm}
            + \xi_{Qm} \odot \xi_{Rm}]\.
    </p>
  </body>
</html>

### 1-1.Using subtraction to calculate FITS_CC:
<html>
  <body>
    <p>
      Except for \(\widehat{\mathbf{K}}_Q\) and \(\widehat{\mathbf{K}}_R\), we introduce
      a new fingerprint \(\widehat{\mathbf{K}}_Z\), which is extracted from images of another device with the same model and post-processing software,
    </p>
    <p>
      \[\widehat{\mathbf{K}}_Z = \alpha_Z \mathbf{K}_Z + \beta_Z \mathbf{S}_Z + \xi_Z\].
    </p>
    <p>  
      FITS_CC can be expressed as follows,
    </p>
    <p>
      \[\operatorname{FITS\_CC_1} = \operatorname{CC}(\widehat{\mathbf{K}}_Q,\widehat{\mathbf{K}}_R) 
      - \operatorname{CC}(\widehat{\mathbf{K}}_Q,\widehat{\mathbf{K}}_Z) $
      \begin{equation}
      = \alpha_Q \alpha_R \mathbf{K}_{Qm} \odot \mathbf{K}_{Rm}
      + \beta_Q \beta_R \mathbf{S}_{Qm} \odot \mathbf{S}_{Rm}
      - \beta_Q \beta_Z \mathbf{S}_{Qm} \odot \mathbf{S}_{Zm}
      +  \varphi_{QRZ},
      \end{equation}\]
    </p>
    <p>
      where
    </p>
    <p>
      \[\varphi_{QRZ} = \varphi_{QR} + \varphi_{QZ} - \alpha_Q \alpha_Z \mathbf{K}_{Qm} \odot \mathbf{K}_{Zm}\].
    </p>
    <p>
      Please note that \(\mathbf{K}_{Qm}\) and \(\mathbf{K}_{Zm}\) are hardware fingerprints from different devices. Therefore \(\mathbf{K}_{Qm} \odot \mathbf{K}_{Zm}\) is included in the combination of random noises \(\varphi_{QRZ}\). 
      Since the mean of random noise \(\varphi_{QRZ}\) is statistically close to zero, we ignore \(\varphi_{QRZ}\) and Equation (\ref{eq:CC_Sub_0}) can be further simplified as:
    </p>
    <p>
      \[\operatorname{FITS\_CC_1} \approx
      \alpha_Q \alpha_R \mathbf{K}_{Qm} \odot \mathbf{K}_{Rm}
      + \beta_Q \beta_R \mathbf{S}_{Qm} \odot \mathbf{S}_{Rm}
      - \beta_Q \beta_Z \mathbf{S}_{Qm} \odot \mathbf{S}_{Zm}\].
    </p>
  </body>
</html>




Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](./another-page.html).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
