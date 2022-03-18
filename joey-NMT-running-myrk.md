# Joey-NMT Running with Myanmar-Rakhine Parallel Data

Joey-NMT ကို ကိုယ်ဒေတာနဲ့ကိုယ် run တတ်အောင် ဥပမာအနေနဲ့ run ပြထား...  

လောလောဆယ် joey-nmt ရဲ့ RNN မော်ဒယ်နဲ့ MT performance ကို ကြည့်ကြည့်မယ်...  
အချိန်ဘယ်လောက် ကြာမယ် ဆိုတာကိုလည်း သိချင်တယ်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/small.myrk.yaml 
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 16:56:01,610 - INFO - joeynmt.training - Epoch   1, Step:     1160, Batch Loss:     3.408352, Tokens per Sec:      834, Lr: 0.000156
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Example #0
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Hypothesis: <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk>
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Example #1
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Hypothesis: <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk>
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Example #2
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-26 16:56:08,125 - INFO - joeynmt.training - 	Hypothesis: <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk> <unk>
2022-02-26 16:56:08,125 - INFO - joeynmt.training - Validation result (greedy) at epoch   1, step     1160: bleu:   0.00, loss: 3581.4941, ppl:   1.3005, duration: 6.5147s
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4100 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4102 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4150 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4146 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4096 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4155 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4142 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4119 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4156 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4106 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4101 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4140 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4129 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4143 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4117 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4154 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4125 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4122 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4121 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 16:56:08,866 - INFO - joeynmt.training - Training ended since minimum lr 0.0001 was reached.
2022-02-26 16:56:08,867 - INFO - joeynmt.training - Best validation result (greedy) at step     1040: 3579.62 loss.
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/1040.ckpt
2022-02-26 16:56:08,886 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 16:56:08,889 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 16:56:08,890 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.dev
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-26 16:56:44,886 - INFO - joeynmt.prediction - test bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:44,887 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.test

real	18m17.359s
user	118m39.958s
sys	2m28.652s

```

၁၈ မိနစ်ခန့်ပဲ ကြာတယ်။  

## Testing with RNN Model for My-RK

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt translate configs/small.myrk.yaml < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./models/small_model_myrk/myrk.syl.out
2022-02-26 17:06:02,582 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 17:06:02,611 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/latest.ckpt
2022-02-26 17:06:02,615 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 17:06:02,618 - INFO - joeynmt.model - Enc-dec model built.

real	0m20.380s
user	2m20.991s
sys	0m0.875s
(joey) ye@:~/exp/joeynmt$
```

### Check the Log Files

```
2022-02-26 16:56:08,731 - DEBUG - matplotlib.backends.backend_pdf - Writing TrueType font.
2022-02-26 16:56:08,866 - INFO - joeynmt.training - Training ended since minimum lr 0.0001 was reached.
2022-02-26 16:56:08,867 - INFO - joeynmt.training - Best validation result (greedy) at step     1040: 3579.62 loss.
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-26 16:56:08,883 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/1040.ckpt
2022-02-26 16:56:08,886 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 16:56:08,889 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 16:56:08,890 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.dev
2022-02-26 16:56:21,160 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-26 16:56:44,886 - INFO - joeynmt.prediction - test bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 16:56:44,887 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00001040.hyps.test
(joey) ye@:~/exp/joeynmt/models/small_model_myrk$ cat ./validations.txt 
Steps: 10	Loss: 63616.55078	PPL: 106.45625	bleu: 0.00000	LR: 0.00500000	*
Steps: 20	Loss: 26462.26172	PPL: 6.96999	bleu: 0.00000	LR: 0.00500000	*
Steps: 30	Loss: 6819.06641	PPL: 1.64927	bleu: 0.00000	LR: 0.00500000	*
Steps: 40	Loss: 4358.31396	PPL: 1.37683	bleu: 0.00000	LR: 0.00500000	*
Steps: 50	Loss: 3905.57471	PPL: 1.33184	bleu: 0.00000	LR: 0.00500000	*
Steps: 60	Loss: 3798.10986	PPL: 1.32138	bleu: 0.00000	LR: 0.00500000	*
Steps: 70	Loss: 3683.61304	PPL: 1.31033	bleu: 0.00000	LR: 0.00500000	*
Steps: 80	Loss: 3674.39038	PPL: 1.30944	bleu: 0.00000	LR: 0.00500000	*
Steps: 90	Loss: 3664.30811	PPL: 1.30847	bleu: 0.00000	LR: 0.00500000	*
Steps: 100	Loss: 3639.98413	PPL: 1.30614	bleu: 0.00000	LR: 0.00500000	*
Steps: 110	Loss: 3637.31250	PPL: 1.30588	bleu: 0.00000	LR: 0.00500000	*
Steps: 120	Loss: 3627.07373	PPL: 1.30490	bleu: 0.00000	LR: 0.00500000	*
Steps: 130	Loss: 3622.11011	PPL: 1.30443	bleu: 0.00000	LR: 0.00500000	*
Steps: 140	Loss: 3617.94604	PPL: 1.30403	bleu: 0.00000	LR: 0.00500000	*
Steps: 150	Loss: 3617.85791	PPL: 1.30402	bleu: 0.00000	LR: 0.00500000	*
Steps: 160	Loss: 3613.80103	PPL: 1.30363	bleu: 0.00000	LR: 0.00500000	*
Steps: 170	Loss: 3608.61084	PPL: 1.30314	bleu: 0.00000	LR: 0.00500000	*
Steps: 180	Loss: 3605.76758	PPL: 1.30287	bleu: 0.00000	LR: 0.00500000	*
Steps: 190	Loss: 3604.20532	PPL: 1.30272	bleu: 0.00000	LR: 0.00500000	*
Steps: 200	Loss: 3611.28711	PPL: 1.30339	bleu: 0.00000	LR: 0.00500000	
Steps: 210	Loss: 3601.01953	PPL: 1.30241	bleu: 0.00000	LR: 0.00500000	*
Steps: 220	Loss: 3609.77881	PPL: 1.30325	bleu: 0.00000	LR: 0.00500000	
Steps: 230	Loss: 3597.10034	PPL: 1.30204	bleu: 0.00000	LR: 0.00500000	*
Steps: 240	Loss: 3595.85669	PPL: 1.30192	bleu: 0.00000	LR: 0.00500000	*
Steps: 250	Loss: 3605.42236	PPL: 1.30283	bleu: 0.00000	LR: 0.00500000	
Steps: 260	Loss: 3596.00537	PPL: 1.30193	bleu: 0.00000	LR: 0.00500000	
Steps: 270	Loss: 3598.31812	PPL: 1.30215	bleu: 0.00000	LR: 0.00500000	
Steps: 280	Loss: 3591.86255	PPL: 1.30154	bleu: 0.00000	LR: 0.00500000	*
Steps: 290	Loss: 3591.77832	PPL: 1.30153	bleu: 0.00000	LR: 0.00500000	*
Steps: 300	Loss: 3590.96387	PPL: 1.30145	bleu: 0.00000	LR: 0.00500000	*
Steps: 310	Loss: 3590.57886	PPL: 1.30141	bleu: 0.00000	LR: 0.00500000	*
Steps: 320	Loss: 3598.61182	PPL: 1.30218	bleu: 0.00000	LR: 0.00500000	
Steps: 330	Loss: 3604.26172	PPL: 1.30272	bleu: 0.00000	LR: 0.00500000	
Steps: 340	Loss: 3587.80713	PPL: 1.30115	bleu: 0.00000	LR: 0.00500000	*
Steps: 350	Loss: 3587.35400	PPL: 1.30111	bleu: 0.00000	LR: 0.00500000	*
Steps: 360	Loss: 3591.36426	PPL: 1.30149	bleu: 0.00000	LR: 0.00500000	
Steps: 370	Loss: 3586.71948	PPL: 1.30105	bleu: 0.00000	LR: 0.00500000	*
Steps: 380	Loss: 3587.64160	PPL: 1.30113	bleu: 0.00000	LR: 0.00500000	
Steps: 390	Loss: 3586.05933	PPL: 1.30098	bleu: 0.00000	LR: 0.00500000	*
Steps: 400	Loss: 3588.46240	PPL: 1.30121	bleu: 0.00000	LR: 0.00500000	
Steps: 410	Loss: 3591.14600	PPL: 1.30147	bleu: 0.00000	LR: 0.00500000	
Steps: 420	Loss: 3584.80835	PPL: 1.30086	bleu: 0.00000	LR: 0.00500000	*
Steps: 430	Loss: 3584.30103	PPL: 1.30081	bleu: 0.00000	LR: 0.00500000	*
Steps: 440	Loss: 3584.98682	PPL: 1.30088	bleu: 0.00000	LR: 0.00500000	
Steps: 450	Loss: 3587.60474	PPL: 1.30113	bleu: 0.00000	LR: 0.00500000	
Steps: 460	Loss: 3586.50366	PPL: 1.30102	bleu: 0.00000	LR: 0.00500000	
Steps: 470	Loss: 3585.23682	PPL: 1.30090	bleu: 0.00000	LR: 0.00500000	
Steps: 480	Loss: 3589.81104	PPL: 1.30134	bleu: 0.00000	LR: 0.00500000	
Steps: 490	Loss: 3582.60669	PPL: 1.30065	bleu: 0.00000	LR: 0.00500000	*
Steps: 500	Loss: 3584.86279	PPL: 1.30087	bleu: 0.00000	LR: 0.00500000	
Steps: 510	Loss: 3582.95288	PPL: 1.30069	bleu: 0.00000	LR: 0.00500000	
Steps: 520	Loss: 3582.91504	PPL: 1.30068	bleu: 0.00000	LR: 0.00500000	
Steps: 530	Loss: 3585.79395	PPL: 1.30096	bleu: 0.00000	LR: 0.00500000	
Steps: 540	Loss: 3583.24780	PPL: 1.30071	bleu: 0.00000	LR: 0.00500000	
Steps: 550	Loss: 3607.86914	PPL: 1.30307	bleu: 0.00000	LR: 0.00250000	
Steps: 560	Loss: 3581.30029	PPL: 1.30053	bleu: 0.00000	LR: 0.00250000	*
Steps: 570	Loss: 3582.43359	PPL: 1.30064	bleu: 0.00000	LR: 0.00250000	
Steps: 580	Loss: 3582.40527	PPL: 1.30063	bleu: 0.00000	LR: 0.00250000	
Steps: 590	Loss: 3581.04492	PPL: 1.30050	bleu: 0.00000	LR: 0.00250000	*
Steps: 600	Loss: 3583.27319	PPL: 1.30072	bleu: 0.00000	LR: 0.00250000	
Steps: 610	Loss: 3583.37524	PPL: 1.30073	bleu: 0.00000	LR: 0.00250000	
Steps: 620	Loss: 3585.72192	PPL: 1.30095	bleu: 0.00000	LR: 0.00250000	
Steps: 630	Loss: 3581.77051	PPL: 1.30057	bleu: 0.00000	LR: 0.00250000	
Steps: 640	Loss: 3593.86060	PPL: 1.30173	bleu: 0.00000	LR: 0.00250000	
Steps: 650	Loss: 3586.39160	PPL: 1.30101	bleu: 0.00000	LR: 0.00125000	
Steps: 660	Loss: 3580.96167	PPL: 1.30050	bleu: 0.00000	LR: 0.00125000	*
Steps: 670	Loss: 3587.34399	PPL: 1.30111	bleu: 0.00000	LR: 0.00125000	
Steps: 680	Loss: 3581.25903	PPL: 1.30052	bleu: 0.00000	LR: 0.00125000	
Steps: 690	Loss: 3580.80737	PPL: 1.30048	bleu: 0.00000	LR: 0.00125000	*
Steps: 700	Loss: 3580.80493	PPL: 1.30048	bleu: 0.00000	LR: 0.00125000	*
Steps: 710	Loss: 3583.26343	PPL: 1.30072	bleu: 0.00000	LR: 0.00125000	
Steps: 720	Loss: 3583.63428	PPL: 1.30075	bleu: 0.00000	LR: 0.00125000	
Steps: 730	Loss: 3580.36914	PPL: 1.30044	bleu: 0.00000	LR: 0.00125000	*
Steps: 740	Loss: 3580.51953	PPL: 1.30045	bleu: 0.00000	LR: 0.00125000	
Steps: 750	Loss: 3588.47485	PPL: 1.30121	bleu: 0.00000	LR: 0.00125000	
Steps: 760	Loss: 3580.10107	PPL: 1.30041	bleu: 0.00000	LR: 0.00125000	*
Steps: 770	Loss: 3580.17139	PPL: 1.30042	bleu: 0.00000	LR: 0.00125000	
Steps: 780	Loss: 3590.39038	PPL: 1.30140	bleu: 0.00000	LR: 0.00125000	
Steps: 790	Loss: 3580.57349	PPL: 1.30046	bleu: 0.00000	LR: 0.00125000	
Steps: 800	Loss: 3580.10400	PPL: 1.30041	bleu: 0.00000	LR: 0.00125000	
Steps: 810	Loss: 3581.50732	PPL: 1.30055	bleu: 0.00000	LR: 0.00125000	
Steps: 820	Loss: 3580.26855	PPL: 1.30043	bleu: 0.00000	LR: 0.00062500	
Steps: 830	Loss: 3581.93774	PPL: 1.30059	bleu: 0.00000	LR: 0.00062500	
Steps: 840	Loss: 3580.07007	PPL: 1.30041	bleu: 0.00000	LR: 0.00062500	*
Steps: 850	Loss: 3579.92676	PPL: 1.30040	bleu: 0.00000	LR: 0.00062500	*
Steps: 860	Loss: 3579.88745	PPL: 1.30039	bleu: 0.00000	LR: 0.00062500	*
Steps: 870	Loss: 3581.90942	PPL: 1.30059	bleu: 0.00000	LR: 0.00062500	
Steps: 880	Loss: 3580.43994	PPL: 1.30045	bleu: 0.00000	LR: 0.00062500	
Steps: 890	Loss: 3579.80542	PPL: 1.30039	bleu: 0.00000	LR: 0.00062500	*
Steps: 900	Loss: 3579.78125	PPL: 1.30038	bleu: 0.00000	LR: 0.00062500	*
Steps: 910	Loss: 3579.90088	PPL: 1.30039	bleu: 0.00000	LR: 0.00062500	
Steps: 920	Loss: 3581.22998	PPL: 1.30052	bleu: 0.00000	LR: 0.00062500	
Steps: 930	Loss: 3580.48633	PPL: 1.30045	bleu: 0.00000	LR: 0.00062500	
Steps: 940	Loss: 3580.79810	PPL: 1.30048	bleu: 0.00000	LR: 0.00062500	
Steps: 950	Loss: 3580.71533	PPL: 1.30047	bleu: 0.00000	LR: 0.00062500	
Steps: 960	Loss: 3579.79126	PPL: 1.30038	bleu: 0.00000	LR: 0.00031250	
Steps: 970	Loss: 3580.28101	PPL: 1.30043	bleu: 0.00000	LR: 0.00031250	
Steps: 980	Loss: 3580.50073	PPL: 1.30045	bleu: 0.00000	LR: 0.00031250	
Steps: 990	Loss: 3579.73975	PPL: 1.30038	bleu: 0.00000	LR: 0.00031250	*
Steps: 1000	Loss: 3579.98120	PPL: 1.30040	bleu: 0.00000	LR: 0.00031250	
Steps: 1010	Loss: 3580.55859	PPL: 1.30046	bleu: 0.00000	LR: 0.00031250	
Steps: 1020	Loss: 3582.33203	PPL: 1.30063	bleu: 0.00000	LR: 0.00031250	
Steps: 1030	Loss: 3581.53589	PPL: 1.30055	bleu: 0.00000	LR: 0.00031250	
Steps: 1040	Loss: 3579.61597	PPL: 1.30037	bleu: 0.00000	LR: 0.00031250	*
Steps: 1050	Loss: 3579.63818	PPL: 1.30037	bleu: 0.00000	LR: 0.00031250	
Steps: 1060	Loss: 3580.41138	PPL: 1.30044	bleu: 0.00000	LR: 0.00031250	
Steps: 1070	Loss: 3582.11206	PPL: 1.30061	bleu: 0.00000	LR: 0.00031250	
Steps: 1080	Loss: 3582.06348	PPL: 1.30060	bleu: 0.00000	LR: 0.00031250	
Steps: 1090	Loss: 3581.48877	PPL: 1.30055	bleu: 0.00000	LR: 0.00031250	
Steps: 1100	Loss: 3581.87061	PPL: 1.30058	bleu: 0.00000	LR: 0.00015625	
Steps: 1110	Loss: 3581.00659	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1120	Loss: 3580.96680	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1130	Loss: 3581.01660	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1140	Loss: 3580.28760	PPL: 1.30043	bleu: 0.00000	LR: 0.00015625	
Steps: 1150	Loss: 3580.99316	PPL: 1.30050	bleu: 0.00000	LR: 0.00015625	
Steps: 1160	Loss: 3581.49414	PPL: 1.30055	bleu: 0.00000	LR: 0.00007813	
(joey) ye@:~/exp/joeynmt/models/small_model_myrk$ cat ./translate.log 
2022-02-26 17:06:02,582 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 17:06:02,611 - DEBUG - joeynmt.prediction - Process device: cpu, n_gpu: 0
2022-02-26 17:06:02,611 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/latest.ckpt
2022-02-26 17:06:02,615 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 17:06:02,618 - INFO - joeynmt.model - Enc-dec model built.
(joey) ye@:~/exp/joeynmt/models/small_model_myrk$
```

log ဖိုင်တွေကို ကြည့်တော့ BLEU score တွေက zero အဆင့်မှာပဲ ရှိသေးတော့ configuration ဖိုင်ကို ပြန်ကြည့်ပြီး update လုပ်သင့်တာ လုပ်ရလိမ့်မယ်လို့ ထင်တယ်...  

## Learn Small Config File and Updating

ပထမ run တုန်းက vocab ဖိုင်ကို marian တုန်းက ဆောက်ခဲ့တဲ့ vocab ဖိုင်ကို assign လုပ်ခဲ့တာ...  

```
src_vocab: "/media/ye/project2/exp/myrk-transformer/data/syl/vocab/vocab.my.yml"
    # trg_vocab: "my_model/trg_vocab.txt"  # one token per line, line number is index            
    trg_vocab: "/media/ye/project2/exp/myrk-transformer/data/syl/vocab/vocab.rk.yml"
```

အဲဒါကို ပိတ်ကြည့်မယ် ...  

ပထမ run တုန်းက epochs: 1, Validation_freq: 10 ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်...  

```
epochs: 30                       # train for this many epochs
validation_freq: 1000             # validate after this many updates (number of mini-batches), default: 1000
```
    
loging freq ကိုလည်း ၁၀ ကနေ ၁၀၀ အဖြစ် ပြောင်းခဲ့တယ်...   

```
logging_freq: 100                # log the training progress after this many updates, default: 100
```

ပြီးတော့... GPU ပါ သုံးကြည့်မယ်  

```
    use_cuda: True                 # use CUDA for acceleration on GPU, required. Set to False when working on CPU.
```

## ReTraining RNN with JoeyNMt for RK-MY (Syllable)

အထက်ပါအတိုင်း config ဖိုင်ကို update လုပ်ပြီးနောက် ထပ် training လုပ်ကြည့်ခဲ့...  

```
(joey) ye@:~/exp/joeynmt/configs$ vi ./transformer_copy.yaml 
(joey) ye@:~/exp/joeynmt/configs$ 
(joey) ye@:~/exp/joeynmt/configs$ cd ..
(joey) ye@:~/exp/joeynmt$ 
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/small.myrk.yaml 
2022-02-26 17:20:11,561 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 17:20:11,578 - INFO - joeynmt.data - Loading training data...
2022-02-26 17:20:11,778 - INFO - joeynmt.data - Building vocabulary...
2022-02-26 17:20:11,855 - INFO - joeynmt.data - Loading dev data...
2022-02-26 17:20:11,866 - INFO - joeynmt.data - Loading test data...
2022-02-26 17:20:11,885 - INFO - joeynmt.data - Data loaded.
2022-02-26 17:20:11,885 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 17:20:11,888 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 17:20:11.966605: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-26 17:20:12,675 - INFO - joeynmt.training - Total params: 161104
2022-02-26 17:20:12,676 - WARNING - joeynmt.training - `keep_last_ckpts` option is outdated. Please use `keep_best_ckpts`, instead.
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                           cfg.name : my_experiment
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.data.random_train_subset : -1
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 30
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 1
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 1
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 5
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -            cfg.testing.postprocess : True
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -               cfg.testing.bpe_type : subword-nmt
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers - cfg.testing.sacrebleu.remove_whitespace : True
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -     cfg.testing.sacrebleu.tokenize : 13a
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.training.reset_best_ckpt : False
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.training.reset_scheduler : False
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -       cfg.training.reset_optimizer : False
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -            cfg.training.adam_betas : [0.9, 0.999]
2022-02-26 17:20:12,676 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.005
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 0.0001
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -         cfg.training.clip_grad_val : 1.0
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -            cfg.training.batch_size : 10
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -            cfg.training.batch_type : sentence
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.eval_batch_size : 10
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.eval_batch_type : sentence
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -      cfg.training.batch_multiplier : 1
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -         cfg.training.normalization : batch
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -              cfg.training.patience : 5
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -                cfg.training.epochs : 30
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : loss
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/small_model_myrk
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -              cfg.training.use_cuda : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -                  cfg.training.fp16 : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 31
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2]
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.keep_last_ckpts : 3
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers -       cfg.training.label_smoothing : 0.0
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.use_reinforcement_learning : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.method : reinforce
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.log_probabilities : True
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.pickle_logs : False
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.topk : 20
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.temperature : 1
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.reward : bleu
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.baseline : average_reward_baseline
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.alpha : 0.005
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.samples : 5
2022-02-26 17:20:12,677 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.add_gold : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.training.reinforcement_learning.hyperparameters.critic_learning_rate : 5e-06
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -              cfg.model.initializer : xavier
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -              cfg.model.init_weight : 0.01
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -                cfg.model.init_gain : 1.0
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.bias_initializer : zeros
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -        cfg.model.embed_initializer : normal
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -        cfg.model.embed_init_weight : 0.1
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.embed_init_gain : 1.0
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.init_rnn_orthogonal : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.lstm_forget_gate : 1.0
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.tied_embeddings : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -             cfg.model.tied_softmax : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -             cfg.model.encoder.type : recurrent
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : gru
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 16
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.freeze : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 30
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 3
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -           cfg.model.encoder.freeze : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -             cfg.model.decoder.type : recurrent
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : gru
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.freeze : False
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 30
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 2
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : last
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : bahdanau
2022-02-26 17:20:12,678 - INFO - joeynmt.helpers -           cfg.model.decoder.freeze : False
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - Data set sizes: 
	train 15324,
	valid 1000,
	test 1811
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) ကို (7) အ (8) တယ် (9) သူ
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) မ (8) ရေ (9) ပါ
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - Number of Src words (types): 1552
2022-02-26 17:20:12,679 - INFO - joeynmt.helpers - Number of Trg words (types): 1662
2022-02-26 17:20:12,679 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(GRU(16, 30, num_layers=3, batch_first=True, dropout=0.2, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=GRU(46, 30, num_layers=2, batch_first=True, dropout=0.2), attention=BahdanauAttention),
	src_embed=Embeddings(embedding_dim=16, vocab_size=1552),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=1662))
2022-02-26 17:20:12,680 - INFO - joeynmt.training - Train stats:
	device: cpu
	n_gpu: 0
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 10
	total batch size (w. parallel & accumulation): 10
2022-02-26 17:20:12,680 - INFO - joeynmt.training - EPOCH 1
2022-02-26 17:20:20,858 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    72.434441, Tokens per Sec:     1626, Lr: 0.005000
...
...
...
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4118 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4141 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 17:59:32,673 - INFO - joeynmt.training - Epoch  16, Step:    24100, Batch Loss:    33.629875, Tokens per Sec:     1509, Lr: 0.005000
2022-02-26 17:59:40,632 - INFO - joeynmt.training - Epoch  16, Step:    24200, Batch Loss:    44.099648, Tokens per Sec:     1659, Lr: 0.005000
2022-02-26 17:59:49,927 - INFO - joeynmt.training - Epoch  16, Step:    24300, Batch Loss:    25.616074, Tokens per Sec:     1410, Lr: 0.005000
2022-02-26 17:59:59,881 - INFO - joeynmt.training - Epoch  16, Step:    24400, Batch Loss:    35.911987, Tokens per Sec:     1321, Lr: 0.005000
2022-02-26 18:00:09,425 - INFO - joeynmt.training - Epoch  16, Step:    24500, Batch Loss:    40.154503, Tokens per Sec:     1395, Lr: 0.005000
2022-02-26 18:00:12,227 - INFO - joeynmt.training - Epoch  16: total training loss 53995.52
2022-02-26 18:00:12,228 - INFO - joeynmt.training - EPOCH 17
2022-02-26 18:00:19,006 - INFO - joeynmt.training - Epoch  17, Step:    24600, Batch Loss:    45.319824, Tokens per Sec:     1426, Lr: 0.005000
2022-02-26 18:00:28,422 - INFO - joeynmt.training - Epoch  17, Step:    24700, Batch Loss:    48.196053, Tokens per Sec:     1407, Lr: 0.005000
2022-02-26 18:00:37,692 - INFO - joeynmt.training - Epoch  17, Step:    24800, Batch Loss:    41.469799, Tokens per Sec:     1393, Lr: 0.005000
2022-02-26 18:00:46,628 - INFO - joeynmt.training - Epoch  17, Step:    24900, Batch Loss:    33.750587, Tokens per Sec:     1473, Lr: 0.005000
2022-02-26 18:00:56,075 - INFO - joeynmt.training - Epoch  17, Step:    25000, Batch Loss:    33.245201, Tokens per Sec:     1367, Lr: 0.005000
...
...
...
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4151 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
2022-02-26 18:35:02,499 - INFO - joeynmt.training - Epoch  30, Step:    45100, Batch Loss:    41.235615, Tokens per Sec:     1050, Lr: 0.005000
2022-02-26 18:35:14,238 - INFO - joeynmt.training - Epoch  30, Step:    45200, Batch Loss:    34.890701, Tokens per Sec:     1115, Lr: 0.005000
2022-02-26 18:35:26,784 - INFO - joeynmt.training - Epoch  30, Step:    45300, Batch Loss:    28.857077, Tokens per Sec:     1052, Lr: 0.005000
2022-02-26 18:35:40,156 - INFO - joeynmt.training - Epoch  30, Step:    45400, Batch Loss:    25.483398, Tokens per Sec:      995, Lr: 0.005000
2022-02-26 18:35:50,827 - INFO - joeynmt.training - Epoch  30, Step:    45500, Batch Loss:    32.120075, Tokens per Sec:     1242, Lr: 0.005000
2022-02-26 18:35:59,826 - INFO - joeynmt.training - Epoch  30, Step:    45600, Batch Loss:    28.888306, Tokens per Sec:     1471, Lr: 0.005000
2022-02-26 18:36:09,389 - INFO - joeynmt.training - Epoch  30, Step:    45700, Batch Loss:    32.717991, Tokens per Sec:     1363, Lr: 0.005000
2022-02-26 18:36:20,539 - INFO - joeynmt.training - Epoch  30, Step:    45800, Batch Loss:    35.522102, Tokens per Sec:     1172, Lr: 0.005000
2022-02-26 18:36:34,107 - INFO - joeynmt.training - Epoch  30, Step:    45900, Batch Loss:    23.591614, Tokens per Sec:      975, Lr: 0.005000
2022-02-26 18:36:42,320 - INFO - joeynmt.training - Epoch  30: total training loss 49794.87
2022-02-26 18:36:42,320 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-26 18:36:42,320 - INFO - joeynmt.training - Best validation result (greedy) at step    43000: 33397.05 loss.
2022-02-26 18:36:42,338 - INFO - joeynmt.prediction - Process device: cpu, n_gpu: 0, batch_size per device: 10
2022-02-26 18:36:42,338 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/43000.ckpt
2022-02-26 18:36:42,341 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 18:36:42,344 - INFO - joeynmt.model - Enc-dec model built.
2022-02-26 18:36:42,344 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-26 18:36:47,987 - INFO - joeynmt.prediction -  dev bleu[13a]:  20.05 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 18:36:47,987 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00043000.hyps.dev
2022-02-26 18:36:47,987 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-26 18:36:59,325 - INFO - joeynmt.prediction - test bleu[13a]:  19.75 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-26 18:36:59,326 - INFO - joeynmt.prediction - Translations saved to: models/small_model_myrk/00043000.hyps.test

real	76m49.270s
user	543m19.766s
sys	2m3.014s
(joey) ye@:~/exp/joeynmt$ 
```


