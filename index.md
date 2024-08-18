{:.no_toc}
* toc
{:toc}

# Abstract

Singing voice synthesis has achieved remarkable progress in generating natural and high-quality voices. However, existing methods rarely provide precise control over vocal techniques such as mixed voice, falsetto, and breathy tones, limiting the expressive potential of synthetic voices. To address this, we introduce TechSinger, an advanced system for controllable singing voice synthesis that supports five languages and seven vocal techniques. TechSinger employs a flow-matching-based model to accurately reproduce these techniques. To enhance the diversity of training data, we develop a technique detection model that annotates datasets with phoneme-level technique labels. Additionally, our prompt-based technique prediction model enables users to specify desired vocal attributes through natural language, offering fine-grained control over the synthesized singing. Experimental results demonstrate that TechSinger significantly enhances the expressiveness and realism of synthetic singing voices, outperforming existing methods in terms of audio quality and technique-specific control.

![overall](./overall.jpg)

<!-- ---

**Note：** We conduct all tasks in the zero-shot scenario, with training and testing on cross-lingual speech and singing data. 

---

**Dataset**: https://huggingface.co/datasets/GTSinger/GTSinger. For the dataset, we have included a portion of the dataset in the data attachment submitted with the paper. The complete version will be released once the paper is accepted. 

--- -->

# Technique-Controllable Singing Voice Synthesis(SVS)

To assess the performance of TechSinger and baseline models in the technique-controllable singing voice task, we randomly select samples with unseen singers from the test set as targets via different controlling strategies. And in order to represent singing techniques more simply, we use the technique id shown below.

technique: 0 : No Technique; 1 : Mixed Voice; 2 : Falsetto; 3 : Breathy; 4 : Pharyngeal; 5 : Vibrato; 6 : Glissando; 7 : Bubble; 8 : Strong; 9 : Weak
                       


## GT

GT represents the technique controlling strategies that the techniques are obtained from the annotated technique sequences.

**Word:** 抓 不 住 爱 情 的 我 &lt;AP&gt; 总 是 眼 睁 睁 看 它 溜 走

**Phoneme with Technique:** zh(1) ua(1) b(1) u(1) zh(1) u(1) ai(1) q(1) ing(1) d(1) e(1) uo(1) &lt;AP&gt; z(1) ong(1) sh(1) i(1) ian(2) zh(2) eng(2) zh(2) eng(2) k(1) an(1) t(1) a(1) l(1) iou(1,6) z(1) ou(1)


<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/gt/0000.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/diffsinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/visinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/stylesinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/techsinger/0000.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***

**Word:**  想 你 时 你 在 脑 海

**Phoneme with Technique:** x(0) iang(0) n(0) i(0) sh(0) i(0) n(0) i(6) z(0) ai(0) n(0) ao(6) h(0) ai(0)


<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/gt/0001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/diffsinger/0001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/visinger/0001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/stylesinger/0001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/techsinger/0001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***

**Word:**  一 次 就 好 &lt;AP&gt; 我 带 你 去 看 天 荒 地 老

**Phoneme with Technique:** i(1,6) c(1) i(1) j(1) iou(1) h(1) ao(1) &lt;AP&gt; uo(1) d(1) ai(1) n(1) i(1) q(1) u(1) k(1) an(1) t(2,6) ian(2) h(2,6) uang(2) d(2) i(2) l(2,6) ao(2,6)


<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/gt/0002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/diffsinger/0002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/visinger/0002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/stylesinger/0002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/techsinger/0002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***

**Word:** love your curves and all your edges &lt;AP&gt; all your perfect imperfections.

**Phoneme with Technique:** L(1) AH1(1) V(1) Y(1) UH1(1) R(1) K(1) ER1(1) V(1) Z(1) AE1(1) N(1) D(1) AA1(1) L(1) Y(1) UH1(1) R(1) EH1(1) JH(1) IH0(1) Z(1) &lt;AP&gt;(0) AA1(1) L(1) Y(1,6) AO1(1,6) AO1(1,6) R(1,6) P(1) ER1(1) F(1) IH2(1) K(1) T(1) IH2(1) M(1) P(1) ER0(1) F(1) EH1(1) K(1) SH(1) AH0(1) N(1) Z(1) 

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/gt/0003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/diffsinger/0003.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/visinger/0003.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/stylesinger/0003.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/techsinger/0003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

## Random

Random represents the technique controlling strategies that the model generates the techniques automatically and randomly.

**Word:** 我 知 道 &lt;AP&gt; 那 些 夏 天 &lt;AP&gt; 就 像 青 春 一 样 回 不 来

**Phoneme with Technique:** uo(1,7) zh(1) i(1) d(1) ao(1) &lt;AP&gt; n(7) a(7) x(1) ie(1) x(1,3) ia(1,3) t(1,3) ian(1,3) &lt;AP&gt; j(1,7) iou(1,7) x(1) iang(1) q(8) ing(8) ch(8) un(8) i(1,3) iang(1,3) h(1,9) ui(1,9) b(1,9) u(1,9) l(1,9) ai(1,9)


<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/random/diffsinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/random/visinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/random/Stylesinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/random/techsinger/0000.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***


## Prompt-Guided

Prompt-Guided represents the technique controlling strategies that the techniques are predicted by our predictor based on the given prompts.


**Word:** 就 在 那 里 曾 是 你 和 我 &lt;AP&gt; 爱 过 的 地 方

**Phoneme:** j iou z ai n a l i c eng sh i n i h e uo &lt;AP&gt; ai g uo d e d i f ang

Prompt: Generate a Chinese song where a female singer sings in medium vocal range using breathy technique. 


<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/diffsinger/0001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/visinger/0001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/Stylesinger/0001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/techsinger/0001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***


**Word:** 一 壶 清 酒 一 身 尘 灰

**Phoneme:** i h u q ing j iou i sh en ch en h uei

Prompt: Generate a Chinese pop song where a Tenor sings using mixed voice.


<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/diffsinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/visinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/Stylesinger/0000.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/techsinger/0000.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***


**Word:** 一 个 多 情 的 痴 情 的 绝 情 的 无 情 的 人 来 给 我 伤 痕

**Phoneme:** i g e d uo q ing d e ch i q ing d e j ve q ing d e r en l ai g ei uo sh ang h en

Prompt: Create a pop song where a Chinese female singer sings using mixed voice and strong vocal.


<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>DiffSinger</th>
			<th style='text-align: center'>Visinger2</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TechSinger(Ours)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/diffsinger/0002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/visinger/0002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/Stylesinger/0002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/techsinger/0002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

***


4.Target Word: 谁 娶 了 多 愁 善 感 的 你

Prompt: 谁 把 你 的 长 发 盘 起

Successfully transferring the timbre, pronunciation, pitch transition style, and rhythm.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Styler</th>
		<th style='text-align: center'>YourTTS</th>
			<th style='text-align: center'>Mega-TTS</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/styler/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/yourtts/004.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/mega/004.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/004.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

5.Target Word: settled down that you AP found a girl and you AP

Prompt: I head AP that you are AP

Successfully transferring the timbre, pronunciation, pitch transition style, rhythm, and glissando technique.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/005.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/005.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Styler</th>
		<th style='text-align: center'>YourTTS</th>
			<th style='text-align: center'>Mega-TTS</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/styler/005.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/yourtts/005.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/mega/005.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/005.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/005.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

6.Target Word: you belong with me belong with me

Prompt: standing by and waiting at your back door SP all this time how could you not know baby
Successfully transferring the timbre, pronunciation, pitch transition style, rhythm, and vibrato technique.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/prompt/006.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/gt/006.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Styler</th>
		<th style='text-align: center'>YourTTS</th>
			<th style='text-align: center'>Mega-TTS</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/styler/006.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/yourtts/006.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/mega/006.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/style/006.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/svs/tc/006.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---


We add global and phoneme-level text embedding to each baseline model to enable style control. 
Then, we compare TCSinger using multi-level text prompts.
We conduct both parallel and non-parallel experiments according to the target styles.
For global styles, we specify singing methods (bel canto and pop) and emotions (happy and sad) for each test target. 
For phoneme-level styles, we select none, one or more specific techniques (mixed voice, falsetto, breathy, vibrato, glissando, and pharyngeal) for each phoneme of target content. 

## Parallel Style Control

In the parallel experiments, we randomly select unseen audio from the test set, using the GT global style and phoneme-level techniques as the target. 

1.Target Word: 你 是 魔 鬼 中 的 天 使 所 以 送 我 心 碎 的 方 式 AP 是 让 我 笑 到 最 后 AP

Global Text Prompt (Singing Method and Emotion): bel canto, sad

Phoneme-Level Text Prompt (Technique Sequence): 
```
['AP(0)', 'n(1)', 'i(1)', 'sh(1)', 'i(1)', 'm(1)', 'o(1)', 'g(1)', 'uei(1)', 'zh(1)', 'ong(1)', 'd(1)', 'e(1)', 't(1)', 'ian(1)', 'sh(1)', 'i(1)', 's(1)', 'uo(1)', 'i(1)', 's(1)', 'ong(1)', 'uo(1)', 'x(1)', 'in(1)', 's(1)', 'uei(1)', 'd(1)', 'e(1)', 'f(1)', 'ang(1)', 'sh(1)', 'i(1)', 'AP(0)', 'sh(1)', 'i(1)', 'r(1)', 'ang(1)', 'uo(1)', 'x(1)', 'iao(1)', 'd(1)', 'ao(1)', 'z(1)', 'uei(1)', 'h(1)', 'ou(1)', 'AP(0)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

Successfully control global singing method and emotion, and the phoneme-level techniques of glissando and mixed voice.

<table style='width: 20%;'>
	<thead>
		<tr>
		<th style='text-align: center'>Ground Truth</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/text/gt/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Styler</th>
		<th style='text-align: center'>YourTTS</th>
			<th style='text-align: center'>Mega-TTS</th>
			<th style='text-align: center'>StyleSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/text/styler/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/text/yourtts/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/text/mega/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/text/style/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/text/tc/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---

# Ablation Study

we undertake ablation studies to showcase the efficacy of various designs incorporated within TCSinger. 
SAD denotes using the style adaptive decoder or only diffusion decoder, DM means using the duration model in S\&D-LM or using a simple duration predictor of Fastspeech2, and CVQ means using the CVQ model or VQ model in the clustering style encoder.

1.Target Word: 我 的 背 脊 如 荒 丘 而 你 却 微 笑 摆 首 AP 把 它 当 成 整 个 宇 宙 你 与 太 阳 挥 手 也 同 海 鸥 问 候

Prompt: 直 到 那 一 天 SP 你 的 衣 衫 破 旧 而 歌 声 却 温 柔 陪 我 漫 无 目 的 的 四 处 漂 流

Successfully synthesizing the timbre, articulation method, pronunciation, pitch transition style, and rhythm.

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/prompt/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Gronud Truth</th>
			<th style='text-align: center'>TCSinger</th>
			<th style='text-align: center'>w/o SAD</th>
			<th style='text-align: center'>w/o DM</th>
			<th style='text-align: center'>w/o CVQ</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/gt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/tc/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/sad/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/dm/001.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/se/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

2.Target Word: 把 一 个 人 的 温 暖 转 移 到 另 一 个 的 胸 膛 AP 让 上 次 犯 的 错 反 省 出 梦 想 AP 每 个 人 都 是 这 样

Prompt: 才 能 知 道 伤 感 是 爱 的 遗 产 AP 流 浪 过 几 张 双 人 床 换 过 几 次 信 仰 才 让 戒 指 义 无 反 顾 的 交 换 AP

Successfully synthesizing the timbre, articulation method, pronunciation, pitch transition style, and rhythm.

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/prompt/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

<table style='width: 100%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Gronud Truth</th>
			<th style='text-align: center'>TCSinger</th>
			<th style='text-align: center'>w/o SAD</th>
			<th style='text-align: center'>w/o DM</th>
			<th style='text-align: center'>w/o CVQ</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/gt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/tc/002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/sad/002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/dm/002.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/abl/se/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---

# Clustering Style Encoder

In these tests, we utilized the timbre of singer A and the style information of singer B to synthesize results that match the timbre of singer A while differing from that of singer B.
This outcome evidentially shows that our clustering style encoder successfully decouples timbre and style in the mel spectrogram. 

1.Target Word: 我 们 这 些 努 力 不 简 单 快 乐 炼 成 泪 水 是 一 种 勇 敢

Successfully synthesizing the timbre of singer A, the pronunciation, pitch transition style, and rhythm of singer B.

<table style='width: 60%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Singer A</th>
			<th style='text-align: center'>Singer B</th>
			<th style='text-align: center'>Result</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/se/demo1/rt.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/se/demo1/rs.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/se/demo1/re.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

2.Target Word: 这 瞬 眼 的 光 景 最 亲 密 的 距 离 沿 着 你 皮 肤 纹 理

Successfully synthesizing the timbre of singer A, the pronunciation, pitch transition style, and rhythm of singer B.

<table style='width: 60%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Singer A</th>
			<th style='text-align: center'>Singer B</th>
			<th style='text-align: center'>Result</th>
		</tr>
	</thead>
	<tbody>
		<tr>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/se/demo2/rt.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/se/demo2/rs.wav' type='audio/wav'></audio></td>
				<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/se/demo2/re.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---

# Style Control Extended Experiments 

In these tests, we compare different text prompts to show TCSinger's controllability.

## Emotion Difference

Target Word: 东 汉 末 年 分 三 国 SP 烽 火 连 天 不 休

Obviously, TCSinger can control different emotions.

<table style='width: 40%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Happy</th>
			<th style='text-align: center'>Sad</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/extend/000.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/extend/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

## Technique Difference

Target Word: 为 了 爱 孤 军 奋 斗 AP 早 就 吃 够 了 爱 情 的 苦

Obviously, TCSinger can control different techniques for each phoneme.

1.Phoneme-Level Text Prompt (Technique Sequence): 
```
['uei(1)','l(1)','e(1)','ai(1)','g(1)','u(1)','j(1)','vn(1)','f(1)','en(1)','d(1)','ou(1)','AP(0)','z(1)','ao(1)','j(1)','iou(1)','ch(1)','i(1)','g(1)','ou(1)','l(1)','e(1)','ai(1)','q(1)','ing(1)','d(1)','e(1)','k(1)','u(1)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/extend/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

2.Phoneme-Level Text Prompt (Technique Sequence): 
```
['uei(3)','l(3)','e(3)','ai(3)','g(3)','u(3)','j(3)','vn(3)','f(3)','en(3)','d(3)','ou(3)','AP(0)','z(3)','ao(3)','j(3)','iou(3)','ch(3)','i(3)','g(3)','ou(3)','l(3)','e(3)','ai(3)','q(3)','ing(3)','d(3)','e(3)','k(3)','u(3)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

<table style='width: 20%;'>
	<thead>
		<tr>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/extend/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

3.Phoneme-Level Text Prompt (Technique Sequence): 
```
['uei(0)','l(0)','e(0)','ai(0)','g(1)','u(1)','j(1)','vn(1)','f(1)','en(1)','d(1)','ou(1)','AP(0)','z(0)','ao(0)','j(0)','iou(0)','ch(0)','i(0)','g(0)','ou(0)','l(2)','e(2)','ai(2)','q(2)','ing(2)','d(2)','e(2)','k(2)','u(2)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

 <table style='width: 20%;'>
	<thead>
		<tr>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/extend/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

4.Phoneme-Level Text Prompt (Technique Sequence): 
```
['uei(0)','l(0)','e(0)','ai(0)','g(3)','u(3)','j(3)','vn(3)','f(3)','en(3)','d(3)','ou(3)','AP(0)','z(0)','ao(0)','j(0)','iou(0)','ch(0)','i(0)','g(0)','ou(0)','l(0)','e(0)','ai(3)','q(3)','ing(3)','d(3)','e(3)','k(3)','u(3)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

 <table style='width: 20%;'>
	<thead>
		<tr>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/extend/005.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

---

# RMSSinger experiments

In these tests, we utilized RMSSinger, the best traditional SVS model with spk embedding for evaluation.  

## Zero-Shot Style Transfer

1.Target Word: 说 什 么 情 深 似 海 我 却 不 敢 当 AP 最 浪 漫 不 过 与 你 并 肩 看 夕 阳 我 心 之 所 向

Prompt: AP 原 来 所 谓 爱 情 AP 是 这 模 样 AP 就 承 认 一 笑 倾 城 一 见 自 难 忘 AP

TCSinger successfully transfers the timbre, and resonance in pop singing method, pronunciation, rhythm, and pitch transition style.

<table style='width: 80%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
			<th style='text-align: center'>RMSSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/prompt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/gt/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/rms/001.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/tc/001.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

2.Target Word: AP 我 是 只 化 身 孤 岛 的 蓝 鲸 有 着 最 巨 大 的 身 影 AP 鱼 虾 在 身 侧 穿 行

Prompt: 而 大 海 太 平 太 静 多 少 故 事 无 人 倾 听 AP 我 爱 地 中 海 的 天 晴

TCSinger successfully transfers the timbre, and resonance in pop singing method, pronunciation, rhythm, and pitch transition style.

<table style='width: 80%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
			<th style='text-align: center'>RMSSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/prompt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/gt/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/rms/002.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/tc/002.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

## Multi-level Style Control

1.Target Word: SP 向 左 SP 向 右 向 前 看 SP 爱 要 拐 几 个 弯 才 来 SP

Global Text Prompt (Singing Method and Emotion): pop, sad

Phoneme-Level Text Prompt (Technique Sequence): 
```
['SP(0)','x(1)','iang(1)','z(0)','uo(0)','SP(0)','x(2)','iang(2)','iou(2,6)','x(2)','iang(2,6)','q(2)','ian(2)','k(2)','an(2,6)','SP(0)','ai(0)','iao(0)','g(0)','uai(0)','j(0)','i(0)','g(0)','e(0)','uan(0)','c(0)','ai(6)','l(0)','ai(0)','SP(0)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

Successfully control global singing method and emotion, and the phoneme-level techniques of glissando and falsetto.

<table style='width: 60%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Ground Truth</th>
			<th style='text-align: center'>RMSSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/gt/003.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/rms/003.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/tc/003.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

2.Target Word: AP 你 唤 醒 了 我 的 耳 朵 哦 带 走 我 AP

Global Text Prompt (Singing Method and Emotion): bel canto, sad

Phoneme-Level Text Prompt (Technique Sequence): 
```
['AP(0),'n(1)','i(1)','h(1)','uan(1)','x(1)','ing(1)','l(1)','e(1)','uo(1)','d(1)','e(1)','er(1)','d(1)','uo(1,6)','o(1)','d(1)','ai(1,6)','z(1)','ou(1,5,6)','AP(0)']
```

(0: no technique, 1: mix, 2: falsetto, 3: breathy, 4: pharyngeal, 5: vibrato, 6: glissando)

Successfully control global singing method and emotion, and the phoneme-level techniques of vibrato and mixed voice.

<table style='width: 60%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Ground Truth</th>
			<th style='text-align: center'>RMSSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/gt/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/rms/004.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/tc/004.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

## Speech-to-Singing Style Transfer

1.Target Word: I don't care if I know

Prompt: city of stars

TCSinger successfully transfers the timbre, pronunciation, pitch transition style, and rhythm.

<table style='width: 80%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
			<th style='text-align: center'>RMSSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/prompt/005.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/gt/005.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/rms/005.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/tc/005.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

2.Target Word: I'm turning my head up and down

Prompt: yesterday you told me about the blue blue sky

TCSinger successfully transfers the timbre, pronunciation, pitch transition style, and rhythm.

<table style='width: 80%;'>
	<thead>
		<tr>
			<th style='text-align: center'>Prompt</th>
			<th style='text-align: center'>Ground Truth</th>
			<th style='text-align: center'>RMSSinger</th>
			<th style='text-align: center'>TCSinger</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/prompt/006.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/gt/006.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/rms/006.wav' type='audio/wav'></audio></td>
			<td style='text-align: center'><audio controls style='width: 150px;'><source src='wavs/rms/tc/006.wav' type='audio/wav'></audio></td>
		</tr>
	</tbody>
</table>

