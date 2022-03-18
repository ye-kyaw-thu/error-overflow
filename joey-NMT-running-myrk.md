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

## Testing with RNN Model My-RK (Syllable)

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt translate configs/small.myrk.yaml < /media/ye/project2/exp/myrk-transformer/data/syl/test.my > ./models/small_model_myrk/myrk.syl.out2
2022-02-26 18:39:11,691 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-26 18:39:11,722 - INFO - joeynmt.prediction - Loading model from models/small_model_myrk/latest.ckpt
2022-02-26 18:39:11,725 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-26 18:39:11,729 - INFO - joeynmt.model - Enc-dec model built.

real	0m11.509s
user	1m16.510s
sys	0m0.846s
(joey) ye@:~/exp/joeynmt$ head ./models/small_model_myrk/myrk.syl.out2
သူ အ မှန် အ ခါး မ တိ ပီး ပါ လား ။
ကျွန် တော် အ ယောက် လို ပီး ဖို့ ။
ပြ ပြီး ရေ အ တွက် ကို သ င့် ရေ ။
မင်း အ တွက် စိတ် မ ပြော ပါ ။
ထို မ ချေ ကို ထို မ ချေ ဂ ရု မ ဟုတ် ခ ပါ ။
ကိုယ် မင်း ကို လုပ် ခ ပါ ရေ ။
ငါ အ လုပ် မ လုပ် ပါ ။
ကျွန် တော် ဘတ်စ် ရာ ဟိ ရေ အ တွက် အ ထင် ကျွန် တော် ထင် ပါ ။
ည အ ခါး က အ ချိန် မ သူ ရို့ ဇာ စား နီ စွာ လေး ။
မင်း ကိုယ် တိ ကို တွိ နီ ပါ လား ။
(joey) ye@:~/exp/joeynmt$ head /media/ye/project2/exp/myrk-transformer/data/syl/test.rk
သူ အ မှန် အ တိုင်း မ ကျိန် ဆို ရဲ ပါ လား ။
ကျွန် တော် ဆို ကေ ပြန် ပီး လိုက် ဖို့ ။
ဆူ ပြီး ရီ ကို သောက် သ င့် ရေ ။
မင်း မိန်း စ ရာ မ လို ပါ ။
ထို မ ချေ ကို သူ အ မှန် မ မြတ် နိုး ခ ပါ ။
ကိုယ် မင်း ကို နား လည် ပါ ရေ ။
ငါ အ လုပ် မ ပြီး သိ ပါ ။
ငါ ဘတ်စ် ကား စီး ဖို့ အ တွက် အ ကြွီ လို ချင် ရေ ။
မိုး ချက် ချင်း ရွာ ရေ အ ခါ သူ ရို့ ဇာ တိ လုပ် နီ စွာ ။
မင်း တောင် တိ ကို တက် နီ ကျ လား ။
(joey) ye@:~/exp/joeynmt$ 

```

Validation ရလဒ်တွေကို ကြည့်တော့ ပထမဆုံး run တာထက်တော့ တိုးတက်လာတာကို တွေ့ရ...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/small_model_myrk/validations.txt 
Steps: 1000	Loss: 57388.25000	PPL: 67.40676	bleu: 0.52890	LR: 0.00500000	*
Steps: 2000	Loss: 53066.17188	PPL: 49.08836	bleu: 2.10495	LR: 0.00500000	*
Steps: 3000	Loss: 51286.50000	PPL: 43.07927	bleu: 1.86128	LR: 0.00500000	*
Steps: 4000	Loss: 49999.86719	PPL: 39.19848	bleu: 3.05241	LR: 0.00500000	*
Steps: 5000	Loss: 48785.27344	PPL: 35.85632	bleu: 3.38970	LR: 0.00500000	*
Steps: 6000	Loss: 48083.76953	PPL: 34.05743	bleu: 3.76580	LR: 0.00500000	*
Steps: 7000	Loss: 47666.36328	PPL: 33.03019	bleu: 4.05210	LR: 0.00500000	*
Steps: 8000	Loss: 46393.51562	PPL: 30.08508	bleu: 4.76296	LR: 0.00500000	*
Steps: 9000	Loss: 45679.07812	PPL: 28.54863	bleu: 5.94355	LR: 0.00500000	*
Steps: 10000	Loss: 44743.05078	PPL: 26.65375	bleu: 6.83491	LR: 0.00500000	*
Steps: 11000	Loss: 43662.57422	PPL: 24.62229	bleu: 7.07079	LR: 0.00500000	*
Steps: 12000	Loss: 43629.57031	PPL: 24.56274	bleu: 7.94861	LR: 0.00500000	*
Steps: 13000	Loss: 43006.12500	PPL: 23.46445	bleu: 8.60597	LR: 0.00500000	*
Steps: 14000	Loss: 42187.97266	PPL: 22.09731	bleu: 9.23368	LR: 0.00500000	*
Steps: 15000	Loss: 40580.71094	PPL: 19.63918	bleu: 9.68358	LR: 0.00500000	*
Steps: 16000	Loss: 39141.94531	PPL: 17.67162	bleu: 10.84861	LR: 0.00500000	*
Steps: 17000	Loss: 38644.76172	PPL: 17.03859	bleu: 11.43360	LR: 0.00500000	*
Steps: 18000	Loss: 38167.29297	PPL: 16.45200	bleu: 12.91926	LR: 0.00500000	*
Steps: 19000	Loss: 37345.45703	PPL: 15.48926	bleu: 13.24043	LR: 0.00500000	*
Steps: 20000	Loss: 37135.27344	PPL: 15.25222	bleu: 12.98069	LR: 0.00500000	*
Steps: 21000	Loss: 36692.06641	PPL: 14.76420	bleu: 13.46621	LR: 0.00500000	*
Steps: 22000	Loss: 36376.33984	PPL: 14.42611	bleu: 13.95958	LR: 0.00500000	*
Steps: 23000	Loss: 36217.14062	PPL: 14.25858	bleu: 13.78189	LR: 0.00500000	*
Steps: 24000	Loss: 36333.26172	PPL: 14.38058	bleu: 14.53253	LR: 0.00500000	
Steps: 25000	Loss: 35629.09766	PPL: 13.65646	bleu: 14.67296	LR: 0.00500000	*
Steps: 26000	Loss: 35683.49609	PPL: 13.71107	bleu: 14.58215	LR: 0.00500000	
Steps: 27000	Loss: 35626.93750	PPL: 13.65429	bleu: 14.22184	LR: 0.00500000	*
Steps: 28000	Loss: 35178.08594	PPL: 13.21193	bleu: 15.12416	LR: 0.00500000	*
Steps: 29000	Loss: 35752.49219	PPL: 13.78066	bleu: 15.34604	LR: 0.00500000	
Steps: 30000	Loss: 35008.98828	PPL: 13.04902	bleu: 15.54186	LR: 0.00500000	*
Steps: 31000	Loss: 34669.69141	PPL: 12.72817	bleu: 15.22020	LR: 0.00500000	*
Steps: 32000	Loss: 34336.41797	PPL: 12.42070	bleu: 15.56523	LR: 0.00500000	*
Steps: 33000	Loss: 34719.87109	PPL: 12.77512	bleu: 16.37965	LR: 0.00500000	
Steps: 34000	Loss: 35017.46875	PPL: 13.05714	bleu: 15.91264	LR: 0.00500000	
Steps: 35000	Loss: 34258.24219	PPL: 12.34966	bleu: 16.28863	LR: 0.00500000	*
Steps: 36000	Loss: 34083.28516	PPL: 12.19214	bleu: 17.78684	LR: 0.00500000	*
Steps: 37000	Loss: 33634.72656	PPL: 11.79740	bleu: 17.82240	LR: 0.00500000	*
Steps: 38000	Loss: 33990.19922	PPL: 12.10915	bleu: 17.05839	LR: 0.00500000	
Steps: 39000	Loss: 34116.59766	PPL: 12.22198	bleu: 17.18198	LR: 0.00500000	
Steps: 40000	Loss: 34182.85156	PPL: 12.28154	bleu: 17.61039	LR: 0.00500000	
Steps: 41000	Loss: 38095.79688	PPL: 16.36592	bleu: 16.39524	LR: 0.00500000	
Steps: 42000	Loss: 33579.71094	PPL: 11.74988	bleu: 17.89235	LR: 0.00500000	*
Steps: 43000	Loss: 33397.05078	PPL: 11.59345	bleu: 18.63332	LR: 0.00500000	*
Steps: 44000	Loss: 34700.21875	PPL: 12.75671	bleu: 17.97865	LR: 0.00500000	
Steps: 45000	Loss: 33715.35156	PPL: 11.86740	bleu: 17.83172	LR: 0.00500000	
(joey) ye@:~/exp/joeynmt$ 
```

## Training My-RK with wmt_myrk_default.yaml

ဒီတစ်ခါ config ဖိုင်ကို တကယ့် WMT မှာ default အဖြစ် သုံးခဲ့တဲ့ ဖိုင်ကို မြန်မာ-ရခိုင်အတွက် ဝင်ပြင်ပြီး မော်ဒယ်ဆောက်ကြည့်မယ်...  

```
(joey) ye@:~/exp/joeynmt/configs$ cat ./wmt_myrk_default.yaml 
name: "wmt_ende_default"

data:
    src: "my"
    trg: "rk"
    train: "/media/ye/project2/exp/myrk-transformer/data/syl/train"    # training data
    dev: "/media/ye/project2/exp/myrk-transformer/data/syl/dev"        # development data for validation
    test: "/media/ye/project2/exp/myrk-transformer/data/syl/test"      # test data for testing final model; optional    
    level: "word"
    lowercase: False
    max_sent_length: 50
    src_voc_min_freq: 0
    src_voc_limit: 100000
    trg_voc_min_freq: 0
    trg_voc_limit: 100000

testing:
    beam_size: 5
    alpha: 1.0

training:
    random_seed: 42
    optimizer: "adam"
    learning_rate: 0.0003
    learning_rate_min: 0.0000005
    weight_decay: 0.0
    clip_grad_norm: 1.0
    batch_size: 80
    scheduling: "plateau"
    patience: 10
    decrease_factor: 0.5
    early_stopping_metric: "eval_metric"
    epochs: 20
    validation_freq: 7362
    logging_freq: 1000
    eval_metric: "bleu"
    model_dir: "models/wmt_myrk_default"
    overwrite: False
    shuffle: True
    use_cuda: True
    max_output_length: 100
    print_valid_sents: [0, 1, 2]

model:
    encoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 500
            scale: False
        hidden_size: 500
        bidirectional: True
        dropout: 0.2
        num_layers: 1
    decoder:
        rnn_type: "lstm"
        embeddings:
            embedding_dim: 500
            scale: False
        emb_scale: False
        hidden_size: 1000
        dropout: 0.2
        hidden_dropout: 0.2
        num_layers: 1
        input_feeding: True
        init_hidden: "bridge"
        attention: "bahdanau"
(joey) ye@:~/exp/joeynmt/configs$ 
```

run ကြည့်တော့ အောက်ပါအတိုင်း error ပေးတယ်...  

```
2022-02-26 19:02:34,633 - INFO - joeynmt.training - Epoch   6, Step:     1000, Batch Loss:    15.628224, Tokens per Sec:     1821, Lr: 0.000300
2022-02-26 19:04:16,461 - INFO - joeynmt.training - Epoch   6: total training loss 2426.79
2022-02-26 19:04:16,461 - INFO - joeynmt.training - EPOCH 7
2022-02-26 19:06:12,215 - INFO - joeynmt.training - Epoch   7: total training loss 1954.65
2022-02-26 19:06:12,215 - INFO - joeynmt.training - EPOCH 8
2022-02-26 19:08:09,133 - INFO - joeynmt.training - Epoch   8: total training loss 1500.09
2022-02-26 19:08:09,133 - INFO - joeynmt.training - EPOCH 9
2022-02-26 19:10:06,317 - INFO - joeynmt.training - Epoch   9: total training loss 1092.61
2022-02-26 19:10:06,317 - INFO - joeynmt.training - EPOCH 10
2022-02-26 19:12:03,155 - INFO - joeynmt.training - Epoch  10: total training loss 788.03
2022-02-26 19:12:03,155 - INFO - joeynmt.training - EPOCH 11
2022-02-26 19:12:33,894 - INFO - joeynmt.training - Epoch  11, Step:     2000, Batch Loss:     2.603220, Tokens per Sec:     1774, Lr: 0.000300
2022-02-26 19:14:00,143 - INFO - joeynmt.training - Epoch  11: total training loss 618.69
2022-02-26 19:14:00,143 - INFO - joeynmt.training - EPOCH 12
2022-02-26 19:15:57,283 - INFO - joeynmt.training - Epoch  12: total training loss 514.09
2022-02-26 19:15:57,284 - INFO - joeynmt.training - EPOCH 13
2022-02-26 19:17:53,280 - INFO - joeynmt.training - Epoch  13: total training loss 439.72
2022-02-26 19:17:53,280 - INFO - joeynmt.training - EPOCH 14
2022-02-26 19:19:49,555 - INFO - joeynmt.training - Epoch  14: total training loss 381.92
2022-02-26 19:19:49,555 - INFO - joeynmt.training - EPOCH 15
2022-02-26 19:21:45,768 - INFO - joeynmt.training - Epoch  15: total training loss 338.48
2022-02-26 19:21:45,768 - INFO - joeynmt.training - EPOCH 16
2022-02-26 19:22:30,393 - INFO - joeynmt.training - Epoch  16, Step:     3000, Batch Loss:     2.129778, Tokens per Sec:     1824, Lr: 0.000300
2022-02-26 19:23:41,149 - INFO - joeynmt.training - Epoch  16: total training loss 301.70
2022-02-26 19:23:41,149 - INFO - joeynmt.training - EPOCH 17
2022-02-26 19:25:37,394 - INFO - joeynmt.training - Epoch  17: total training loss 268.87
2022-02-26 19:25:37,394 - INFO - joeynmt.training - EPOCH 18
2022-02-26 19:27:34,094 - INFO - joeynmt.training - Epoch  18: total training loss 234.00
2022-02-26 19:27:34,094 - INFO - joeynmt.training - EPOCH 19
2022-02-26 19:29:29,690 - INFO - joeynmt.training - Epoch  19: total training loss 204.30
2022-02-26 19:29:29,690 - INFO - joeynmt.training - EPOCH 20
2022-02-26 19:31:24,889 - INFO - joeynmt.training - Epoch  20: total training loss 180.29
2022-02-26 19:31:24,889 - INFO - joeynmt.training - Training ended after  20 epochs.
2022-02-26 19:31:24,889 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-26 19:31:24,897 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-26 19:31:24,898 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint models/wmt_myrk_default/0.ckpt not found

real	38m57.669s
user	43m24.300s
sys	8m51.045s
(joey) ye@:~/exp/joeynmt$
```

အဲဒါနဲ့ model_dir ရဲ့ path ကို full path ပေးပြီး ပြန် train ခဲ့...  

```
    model_dir: "/home/ye/exp/joeynmt/models/wmt_myrk_default"
```

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 806, in train
    model_dir = make_model_dir(cfg["training"]["model_dir"],
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 44, in make_model_dir
    raise FileExistsError(
FileExistsError: Model directory exists and overwriting is disabled.

real	0m1.694s
user	0m1.063s
sys	0m0.707s
(joey) ye@:~/exp/joeynmt$
```

overwrite ကို True ထားပြီး train မှ ရလိမ့်မယ်...  

```
    overwrite: True
```

train လုပ်ကြည့်တော့ စောစောကလိုပဲ error တက်နေသေးတယ်...?!  

```
2022-02-26 20:34:09,992 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-26 20:34:10,002 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-26 20:34:10,002 - INFO - joeynmt.prediction - Loading model from /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt not found

real	39m6.048s
user	43m45.978s
sys	8m33.931s
(joey) ye@:~/exp/joeynmt$
```

config ဖိုင်ရဲ့ ထိပ်ဆုံး နာမည်ကို original configuration အတိုင်း ထားမိတဲ့ error ကိုတော့ တွေ့ပြီ... အဲဒါကြောင့်လား?!  

```
name: "wmt_ende_default" ကို 
name: "wmt_myrk_default"
```

Error အတူတူပဲ ပေးနေတယ်...  


```
    lowercase: True
```

lowercase ကို True လုပ်ပြီး ထပ် training လုပ်ကြည့်ခဲ့...  

```
2022-02-27 00:13:02,865 - INFO - joeynmt.training - EPOCH 20
2022-02-27 00:14:59,146 - INFO - joeynmt.training - Epoch  20: total training loss 180.29
2022-02-27 00:14:59,146 - INFO - joeynmt.training - Training ended after  20 epochs.
2022-02-27 00:14:59,146 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-27 00:14:59,154 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 00:14:59,154 - INFO - joeynmt.prediction - Loading model from /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint /home/ye/exp/joeynmt/models/wmt_myrk_default/0.ckpt not found

real	39m11.235s
user	43m42.326s
sys	8m45.116s
(joey) ye@:~/exp/joeynmt$ 

```

ဒီ error ပဲ ထပ်ပေးနေတယ်...  

```
    logging_freq: 100
    keep_last_ckpts: 3              # keep this many of the latest checkpoints, if -1: all of them, default: 5
```

small_model_myrk/ ဖိုလ်ဒါအောက်ကို ကြည့်ကြည့်တော့...  
best.ckpt၊ latest.ckpt  နှစ်ဖိုင်ကိုတော့ တွေ့ရတယ်။ training လုပ်နေတဲ့အချိန်မှာတော့ မပြောတတ်ဘူး...  

ထပ် training လုပ်ကြည့်ခဲ့...  
Same ERROR!!!  

code ကို ဝင်ကြည့်တော့ ...  
(File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint)  

```python
    # when checkpoint is not specified, take latest (best) from model dir
    if ckpt is None:
        ckpt = get_latest_checkpoint(model_dir)
        try:
            step = ckpt.split(model_dir+"/")[1].split(".ckpt")[0]
        except IndexError:
            step = "best"
```

path ကို အပြည့်မပေးပဲ run ကြည့်ခဲ့...  

```
#    model_dir: "/home/ye/exp/joeynmt/models/wmt_myrk_default"
    model_dir: "wmt_myrk_default"
```

same error ပဲ ပေးနေ...  
အောက်ပါ configuration parameter သုံးခုကို ပေးခဲ့...  

```
training:
    #load_model: "models/small_model/60.ckpt" # if given, load a pre-trained model from this checkpoint
    reset_best_ckpt: False          # if True, reset the tracking of the best checkpoint and scores. Use for domain adaptation or fine-tuning with new metrics or dev data.
    reset_scheduler: False          # if True, overwrite scheduler in loaded checkpoint with parameters specified in this config. Use for domain adaptation or fine-tuning.
    reset_optimizer: False          # if True, overwrite optimizer in loaded checkpoint with parameters specified in this config. Use for domain adaptation or fine-tuning.
```

debug လုပ်ရတာ မြန်အောင်လို့ epochs: 10 ထားပြီးတော့ ထပ် training လုပ်ကြည့်ခဲ့...  

```
2022-02-27 08:47:15,852 - INFO - joeynmt.training - Epoch  10: total training loss 788.03
2022-02-27 08:47:15,852 - INFO - joeynmt.training - Training ended after  10 epochs.
2022-02-27 08:47:15,852 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-27 08:47:15,862 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 08:47:15,862 - INFO - joeynmt.prediction - Loading model from wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint wmt_myrk_default/0.ckpt not found

real	19m4.202s
user	21m15.634s
sys	4m19.876s
(joey) ye@:~/exp/joeynmt$
```

ဒီတစ်ခါတော့ keep_last_ckpts ဆိုတဲ့ option ကို default value အဖြစ် setting ချိန်ထားခဲ့...  

```
    keep_last_ckpts: 5              # keep this many of the latest checkpoints, if -1: all of them, default: 5
```

model folder ကိုလည်း ဖျက်ခဲ့ပြီး...  

```
(joey) ye@:~/exp/joeynmt/models$ rm -rf wmt_myrk_default/ 
```
ထပ် run ကြည့်ခဲ့...  

```
2022-02-27 09:15:38,744 - INFO - joeynmt.training - Training ended after  10 epochs.
2022-02-27 09:15:38,744 - INFO - joeynmt.training - Best validation result (greedy) at step        0:   -inf eval_metric.
2022-02-27 09:15:38,754 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 09:15:38,755 - INFO - joeynmt.prediction - Loading model from wmt_myrk_default/0.ckpt
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 860, in train
    test(cfg_file,
  File "/home/ye/exp/joeynmt/joeynmt/prediction.py", line 321, in test
    model_checkpoint = load_checkpoint(ckpt, use_cuda=use_cuda)
  File "/home/ye/exp/joeynmt/joeynmt/helpers.py", line 284, in load_checkpoint
    assert os.path.isfile(path), f"Checkpoint {path} not found"
AssertionError: Checkpoint wmt_myrk_default/0.ckpt not found

real	19m4.514s
user	21m17.273s
sys	4m17.999s
(joey) ye@:~/exp/joeynmt$ 
```

WTF! ...  
မော်ဒယ်ကို မဆောက်ပေးနိုင်တာ လို့ ထင်တယ်။ memory မနိုင်တဲ့ error ဘာညာလည်း မပေးပေမဲ့ hidden_size ကို လျှော့ကြည့်ခဲ့...  

```
model:
    encoder:
        hidden_size: 500 ကို
        hidden_size: 30
        
    decoder:
        hidden_size: 30

```

ထပ် run ကြည့်ခဲ့...  
Got ERROR!!!

```
    validation_freq: 7362 ကို
    validation_freq: 1000 ပြောင်း
    
        embeddings:
            embedding_dim: 16    
```
အထက်ပါအတိုင်း parameter တချို့ကို ပြင်ဆင်ပြီးတော့... ထပ် run ကြည့်ခဲ့

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
2022-02-27 10:28:50,418 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-27 10:28:50,435 - INFO - joeynmt.data - Loading training data...
2022-02-27 10:28:50,630 - INFO - joeynmt.data - Building vocabulary...
2022-02-27 10:28:50,706 - INFO - joeynmt.data - Loading dev data...
2022-02-27 10:28:50,717 - INFO - joeynmt.data - Loading test data...
2022-02-27 10:28:50,736 - INFO - joeynmt.data - Data loaded.
2022-02-27 10:28:50,736 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 10:28:50,746 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 10:28:50.824941: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-27 10:28:51,467 - INFO - joeynmt.training - Total params: 1011932
2022-02-27 10:28:51,469 - WARNING - joeynmt.training - `keep_last_ckpts` option is outdated. Please use `keep_best_ckpts`, instead.
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                           cfg.name : wmt_myrk_default
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 50
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100000
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100000
2022-02-27 10:28:53,019 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 5
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.reset_best_ckpt : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.reset_scheduler : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.reset_optimizer : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.0003
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 5e-07
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -            cfg.training.batch_size : 80
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -              cfg.training.patience : 10
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -                cfg.training.epochs : 10
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/wmt_myrk_default
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 100
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2]
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.training.keep_last_ckpts : 5
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 500
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 30
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.2
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 16
2022-02-27 10:28:53,020 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -        cfg.model.decoder.emb_scale : False
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 30
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.2
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.2
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : bridge
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : bahdanau
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - Data set sizes: 
	train 15535,
	valid 1000,
	test 1811
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) အ (7) ကို (8) တယ် (9) သူ
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) ရေ (8) မ (9) ပါ
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - Number of Src words (types): 1580
2022-02-27 10:28:53,021 - INFO - joeynmt.helpers - Number of Trg words (types): 1687
2022-02-27 10:28:53,021 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(500, 30, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(46, 30, batch_first=True), attention=BahdanauAttention),
	src_embed=Embeddings(embedding_dim=500, vocab_size=1580),
	trg_embed=Embeddings(embedding_dim=16, vocab_size=1687))
2022-02-27 10:28:53,022 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 40
	total batch size (w. parallel & accumulation): 80
2022-02-27 10:28:53,022 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 10:29:00,311 - INFO - joeynmt.training - Epoch   1, Step:      100, Batch Loss:    41.147419, Tokens per Sec:    14867, Lr: 0.000300
2022-02-27 10:29:05,484 - INFO - joeynmt.training - Epoch   1: total training loss 8464.12
2022-02-27 10:29:05,484 - INFO - joeynmt.training - EPOCH 2
2022-02-27 10:29:05,765 - INFO - joeynmt.training - Epoch   2, Step:      200, Batch Loss:    34.781780, Tokens per Sec:    19317, Lr: 0.000300
2022-02-27 10:29:11,507 - INFO - joeynmt.training - Epoch   2, Step:      300, Batch Loss:    34.522808, Tokens per Sec:    18908, Lr: 0.000300
2022-02-27 10:29:16,658 - INFO - joeynmt.training - Epoch   2: total training loss 6916.50
2022-02-27 10:29:16,658 - INFO - joeynmt.training - EPOCH 3
2022-02-27 10:29:17,303 - INFO - joeynmt.training - Epoch   3, Step:      400, Batch Loss:    34.547497, Tokens per Sec:    16497, Lr: 0.000300
2022-02-27 10:29:23,244 - INFO - joeynmt.training - Epoch   3, Step:      500, Batch Loss:    34.913837, Tokens per Sec:    18193, Lr: 0.000300
2022-02-27 10:29:28,105 - INFO - joeynmt.training - Epoch   3: total training loss 6710.48
2022-02-27 10:29:28,105 - INFO - joeynmt.training - EPOCH 4
2022-02-27 10:29:28,942 - INFO - joeynmt.training - Epoch   4, Step:      600, Batch Loss:    30.318647, Tokens per Sec:    18848, Lr: 0.000300
2022-02-27 10:29:34,446 - INFO - joeynmt.training - Epoch   4, Step:      700, Batch Loss:    34.668171, Tokens per Sec:    19680, Lr: 0.000300
2022-02-27 10:29:38,987 - INFO - joeynmt.training - Epoch   4: total training loss 6642.92
2022-02-27 10:29:38,987 - INFO - joeynmt.training - EPOCH 5
2022-02-27 10:29:40,095 - INFO - joeynmt.training - Epoch   5, Step:      800, Batch Loss:    35.233486, Tokens per Sec:    19366, Lr: 0.000300
2022-02-27 10:29:45,682 - INFO - joeynmt.training - Epoch   5, Step:      900, Batch Loss:    30.308668, Tokens per Sec:    19306, Lr: 0.000300
2022-02-27 10:29:49,885 - INFO - joeynmt.training - Epoch   5: total training loss 6459.74
2022-02-27 10:29:49,885 - INFO - joeynmt.training - EPOCH 6
2022-02-27 10:29:51,243 - INFO - joeynmt.training - Epoch   6, Step:     1000, Batch Loss:    35.419918, Tokens per Sec:    19812, Lr: 0.000300
2022-02-27 10:29:52,436 - INFO - joeynmt.training - Hooray! New best validation result [eval_metric]!
2022-02-27 10:29:52,453 - INFO - joeynmt.training - Example #0
2022-02-27 10:29:52,453 - INFO - joeynmt.training - 	Source:     မင်း ဆုံး ဖြတ် တဲ့ အ ဖြေ ။
2022-02-27 10:29:52,453 - INFO - joeynmt.training - 	Reference:  မင်း ဆုံး ဖြတ် ရေ အ ဖြေ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Hypothesis: ။ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - Example #1
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Source:     ကျွန် တော် တို့ တီ ဗွီ ကြ ည့် ကြ မယ် ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Reference:  ကျွန် တော် ရို့ တီ ဗွီ ကြ ည့် ကတ် မေ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Hypothesis: ။ ။ ။ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - Example #2
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Source:     စာ အုပ် ဝယ် ဖို့ မေ့ သွား တယ် ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Reference:  စာ အုပ် ဝယ် ဖို့ မိန့် လား ရေ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - 	Hypothesis: ။ ။
2022-02-27 10:29:52,454 - INFO - joeynmt.training - Validation result (greedy) at epoch   6, step     1000: bleu:   0.01, loss: 33062.2891, ppl:  11.3122, duration: 1.2105s
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/_backend_pdf_ps.py:109: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=ft2font.LOAD_NO_HINTING)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:240: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0.0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
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
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 10:29:58,533 - INFO - joeynmt.training - Epoch   6, Step:     1100, Batch Loss:    34.886578, Tokens per Sec:    17815, Lr: 0.000300
2022-02-27 10:30:02,465 - INFO - joeynmt.training - Epoch   6: total training loss 6313.00
2022-02-27 10:30:02,466 - INFO - joeynmt.training - EPOCH 7
2022-02-27 10:30:04,122 - INFO - joeynmt.training - Epoch   7, Step:     1200, Batch Loss:    33.299118, Tokens per Sec:    19435, Lr: 0.000300
2022-02-27 10:30:09,780 - INFO - joeynmt.training - Epoch   7, Step:     1300, Batch Loss:    33.795162, Tokens per Sec:    19147, Lr: 0.000300
2022-02-27 10:30:13,262 - INFO - joeynmt.training - Epoch   7: total training loss 6190.45
2022-02-27 10:30:13,262 - INFO - joeynmt.training - EPOCH 8
2022-02-27 10:30:15,168 - INFO - joeynmt.training - Epoch   8, Step:     1400, Batch Loss:    32.178890, Tokens per Sec:    19892, Lr: 0.000300
2022-02-27 10:30:20,875 - INFO - joeynmt.training - Epoch   8, Step:     1500, Batch Loss:    31.339453, Tokens per Sec:    18946, Lr: 0.000300
2022-02-27 10:30:24,163 - INFO - joeynmt.training - Epoch   8: total training loss 6072.78
2022-02-27 10:30:24,163 - INFO - joeynmt.training - EPOCH 9
2022-02-27 10:30:26,403 - INFO - joeynmt.training - Epoch   9, Step:     1600, Batch Loss:    33.533947, Tokens per Sec:    19340, Lr: 0.000300
2022-02-27 10:30:32,029 - INFO - joeynmt.training - Epoch   9, Step:     1700, Batch Loss:    31.088232, Tokens per Sec:    19315, Lr: 0.000300
2022-02-27 10:30:35,060 - INFO - joeynmt.training - Epoch   9: total training loss 5961.14
2022-02-27 10:30:35,060 - INFO - joeynmt.training - EPOCH 10
2022-02-27 10:30:37,640 - INFO - joeynmt.training - Epoch  10, Step:     1800, Batch Loss:    32.837299, Tokens per Sec:    18733, Lr: 0.000300
2022-02-27 10:30:43,311 - INFO - joeynmt.training - Epoch  10, Step:     1900, Batch Loss:    30.626780, Tokens per Sec:    19128, Lr: 0.000300
2022-02-27 10:30:46,033 - INFO - joeynmt.training - Epoch  10: total training loss 5867.65
2022-02-27 10:30:46,034 - INFO - joeynmt.training - Training ended after  10 epochs.
2022-02-27 10:30:46,034 - INFO - joeynmt.training - Best validation result (greedy) at step     1000:   0.01 eval_metric.
2022-02-27 10:30:46,042 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 10:30:46,042 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/1000.ckpt
2022-02-27 10:30:46,051 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 10:30:46,061 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 10:30:46,065 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 10:30:49,160 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:30:49,160 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00001000.hyps.dev
2022-02-27 10:30:49,160 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 10:30:54,915 - INFO - joeynmt.prediction - test bleu[13a]:   0.00 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:30:54,916 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00001000.hyps.test

real	2m6.122s
user	3m14.651s
sys	0m10.797s
(joey) ye@:~/exp/joeynmt$ 


```

ဒီတစ်ခါတော့ အဆင်ပြေပြေနဲ့ training လုပ်လို့ ရသွားပြီ။ ပြဿနာက "embedding_dim: 16" ကြောင့် ဖြစ်နေတာလို့ ယူဆတယ်...  

model ဖိုလ်ဒါထဲ ဝင်ကြည့်ခဲ့...  
ပုံမှန် အခြေအနေလိုတော့ မြင်ရ  

```
(joey) ye@:~/exp/joeynmt/models/wmt_myrk_default$ ls
00001000.hyps.dev   1000.ckpt  att.1000.0.pdf  att.1000.2.pdf  config.yaml  src_vocab.txt  train.log      validations.txt
00001000.hyps.test  1000.hyps  att.1000.1.pdf  best.ckpt       latest.ckpt  tensorboard    trg_vocab.txt
(joey) ye@:~/exp/joeynmt/models/wmt_myrk_default$ cat validations.txt 
Steps: 1000	Loss: 33062.28906	PPL: 11.31215	bleu: 0.01426	LR: 0.00030000	*
(joey) ye@:~/exp/joeynmt/models/wmt_myrk_default$ 
```

epoch ကို တိုးကြည့်မယ်။ embedding_dim ကိုလည်း တိုးကြည့်မယ်  

```
    epochs: 30
     embedding_dim: 64 # for encoder
      embedding_dim: 64 # for decoder
```

ထပ် run ကြည့်ခဲ့... validation မှာလည်း BLEU က ကောင်းမှ testing မှာလည်း ကောင်းမှာမို့...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
...
...
2022-02-27 10:45:47,871 - INFO - joeynmt.training - Epoch  28, Step:     5300, Batch Loss:    23.637800, Tokens per Sec:    19045, Lr: 0.000300
2022-02-27 10:45:53,455 - INFO - joeynmt.training - Epoch  28, Step:     5400, Batch Loss:    26.368591, Tokens per Sec:    19360, Lr: 0.000300
2022-02-27 10:45:56,743 - INFO - joeynmt.training - Epoch  28: total training loss 5256.34
2022-02-27 10:45:56,743 - INFO - joeynmt.training - EPOCH 29
2022-02-27 10:45:59,000 - INFO - joeynmt.training - Epoch  29, Step:     5500, Batch Loss:    26.696507, Tokens per Sec:    19202, Lr: 0.000300
2022-02-27 10:46:04,673 - INFO - joeynmt.training - Epoch  29, Step:     5600, Batch Loss:    27.197027, Tokens per Sec:    19145, Lr: 0.000300
2022-02-27 10:46:07,611 - INFO - joeynmt.training - Epoch  29: total training loss 5222.24
2022-02-27 10:46:07,612 - INFO - joeynmt.training - EPOCH 30
2022-02-27 10:46:10,097 - INFO - joeynmt.training - Epoch  30, Step:     5700, Batch Loss:    27.575397, Tokens per Sec:    19492, Lr: 0.000300
2022-02-27 10:46:15,590 - INFO - joeynmt.training - Epoch  30, Step:     5800, Batch Loss:    27.157804, Tokens per Sec:    19731, Lr: 0.000300
2022-02-27 10:46:18,336 - INFO - joeynmt.training - Epoch  30: total training loss 5177.38
2022-02-27 10:46:18,336 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-27 10:46:18,336 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:   0.35 eval_metric.
2022-02-27 10:46:18,345 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 10:46:18,345 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/5000.ckpt
2022-02-27 10:46:18,353 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 10:46:18,356 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 10:46:18,358 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 10:46:24,824 - INFO - joeynmt.prediction -  dev bleu[13a]:   0.55 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:46:24,825 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.dev
2022-02-27 10:46:24,825 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 10:46:36,452 - INFO - joeynmt.prediction - test bleu[13a]:   0.76 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 10:46:36,453 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.test

real	5m59.273s
user	9m30.995s
sys	0m30.790s
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
Steps: 1000	Loss: 34432.85938	PPL: 12.50890	bleu: 0.01036	LR: 0.00030000	*
Steps: 2000	Loss: 31097.80469	PPL: 9.79368	bleu: 0.01801	LR: 0.00030000	*
Steps: 3000	Loss: 29530.17773	PPL: 8.72957	bleu: 0.10866	LR: 0.00030000	*
Steps: 4000	Loss: 28522.73047	PPL: 8.10756	bleu: 0.27818	LR: 0.00030000	*
Steps: 5000	Loss: 27801.08008	PPL: 7.68944	bleu: 0.35137	LR: 0.00030000	*
```

တိုးတက်မှုတော့ ရှိတယ် bleu က တအားနည်းနေသေးတယ်...  

```
        hidden_size: 500 ပြန်ထားတယ် encoder အတွက်ရော decoder အတွက်ရော
        embedding_dim: 4096        ကိုလည်း encoder/decoder နှစ်ခုစလုံးအတွက် ထားခဲ့
```

train လုပ်ကြည့်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
...
...
...
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4116 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4124 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4152 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4123 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4145 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4171 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4126 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4157 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/matplotlib/backends/backend_agg.py:203: RuntimeWarning: Glyph 4112 missing from current font.
  font.set_text(s, 0, flags=flags)
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/_functions.py:68: UserWarning: Was asked to gather along dimension 0, but all input tensors were scalars; will instead unsqueeze and return a vector.
  warnings.warn('Was asked to gather along dimension 0, but all '
2022-02-27 11:57:03,712 - INFO - joeynmt.training - Epoch  26: total training loss 113.78
2022-02-27 11:57:03,712 - INFO - joeynmt.training - EPOCH 27
2022-02-27 11:57:27,124 - INFO - joeynmt.training - Epoch  27, Step:     5100, Batch Loss:     0.383438, Tokens per Sec:     1381, Lr: 0.000300
2022-02-27 11:58:42,233 - INFO - joeynmt.training - Epoch  27, Step:     5200, Batch Loss:     0.622168, Tokens per Sec:     1434, Lr: 0.000300
2022-02-27 11:59:31,602 - INFO - joeynmt.training - Epoch  27: total training loss 102.46
2022-02-27 11:59:31,602 - INFO - joeynmt.training - EPOCH 28
2022-02-27 11:59:58,982 - INFO - joeynmt.training - Epoch  28, Step:     5300, Batch Loss:     0.333518, Tokens per Sec:     1392, Lr: 0.000300
2022-02-27 12:01:15,597 - INFO - joeynmt.training - Epoch  28, Step:     5400, Batch Loss:     0.601976, Tokens per Sec:     1411, Lr: 0.000300
2022-02-27 12:02:00,380 - INFO - joeynmt.training - Epoch  28: total training loss 90.95
2022-02-27 12:02:00,380 - INFO - joeynmt.training - EPOCH 29
2022-02-27 12:02:30,506 - INFO - joeynmt.training - Epoch  29, Step:     5500, Batch Loss:     0.261766, Tokens per Sec:     1439, Lr: 0.000300
2022-02-27 12:03:48,839 - INFO - joeynmt.training - Epoch  29, Step:     5600, Batch Loss:     0.489499, Tokens per Sec:     1387, Lr: 0.000300
2022-02-27 12:04:29,301 - INFO - joeynmt.training - Epoch  29: total training loss 82.12
2022-02-27 12:04:29,301 - INFO - joeynmt.training - EPOCH 30
2022-02-27 12:05:03,715 - INFO - joeynmt.training - Epoch  30, Step:     5700, Batch Loss:     0.311833, Tokens per Sec:     1408, Lr: 0.000300
2022-02-27 12:06:19,441 - INFO - joeynmt.training - Epoch  30, Step:     5800, Batch Loss:     0.417136, Tokens per Sec:     1431, Lr: 0.000300
2022-02-27 12:06:56,702 - INFO - joeynmt.training - Epoch  30: total training loss 71.23
2022-02-27 12:06:56,703 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-27 12:06:56,703 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:  82.32 eval_metric.
2022-02-27 12:06:56,731 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 12:06:56,731 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/5000.ckpt
2022-02-27 12:06:57,278 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 12:06:57,671 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 12:06:57,760 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 12:07:40,696 - INFO - joeynmt.prediction -  dev bleu[13a]:  82.53 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 12:07:40,697 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.dev
2022-02-27 12:07:40,697 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 12:08:58,696 - INFO - joeynmt.prediction - test bleu[13a]:  81.63 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 12:08:58,697 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.test

real	78m29.084s
user	91m54.679s
sys	15m15.880s
```

အထက်မှာ မြင်ရတဲ့အတိုင်း... ဒီတစ်ခါတော့ RNN model က ငါတို့ရဲ့ မြန်မာ-ရခိုင် ဒေတာနဲ့ ကောင်းကောင်း အလုပ်လုပ်ပေးတယ်လို့ နားလည်တယ်။  
validation log ဖိုင်ကို ဝင်ကြည့်မယ်...  

```
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
Steps: 1000	Loss: 5521.56543	PPL: 1.49950	bleu: 70.71308	LR: 0.00030000	*
Steps: 2000	Loss: 3119.77002	PPL: 1.25722	bleu: 80.89377	LR: 0.00030000	*
Steps: 3000	Loss: 2918.38110	PPL: 1.23878	bleu: 82.31551	LR: 0.00030000	*
Steps: 4000	Loss: 3539.79443	PPL: 1.29657	bleu: 81.79033	LR: 0.00030000	
Steps: 5000	Loss: 3400.03296	PPL: 1.28335	bleu: 82.32466	LR: 0.00030000	*
(joey) ye@:~/exp/joeynmt$ 
```

လက်ရှိ ပထမဆုံး ရလဒ်ကောင်း၊ သုံးလို့ ရနိုင်လို့ backup ကူးထားခဲ့...  

```
(joey) ye@:~/exp/joeynmt/models$ mv wmt_myrk_default/ wmt_myrk_default1
```

Beam Size ကို တိုးကြည့်မယ်။   

```
testing:
    beam_size: 10 # original setting is 5
    
        hidden_size: 1000 # encoder, decoder နှစ်မျိုးစလုံးအတွက်
```


run ကြည့်မယ်...  

```
(joey) ye@:~/exp/joeynmt$ time python3 -m joeynmt train configs/wmt_myrk_default.yaml 
2022-02-27 12:35:29,616 - INFO - root - Hello! This is Joey-NMT (version 1.5.1).
2022-02-27 12:35:29,636 - INFO - joeynmt.data - Loading training data...
2022-02-27 12:35:32,624 - INFO - joeynmt.data - Building vocabulary...
2022-02-27 12:35:32,703 - INFO - joeynmt.data - Loading dev data...
2022-02-27 12:35:32,726 - INFO - joeynmt.data - Loading test data...
2022-02-27 12:35:32,747 - INFO - joeynmt.data - Data loaded.
2022-02-27 12:35:32,747 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 12:35:33,505 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 12:35:33.773895: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-02-27 12:35:34,955 - INFO - joeynmt.training - Total params: 88247632
2022-02-27 12:35:34,956 - WARNING - joeynmt.training - `keep_last_ckpts` option is outdated. Please use `keep_best_ckpts`, instead.
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                           cfg.name : wmt_myrk_default
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                       cfg.data.src : my
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                       cfg.data.trg : rk
2022-02-27 12:35:37,360 - INFO - joeynmt.helpers -                     cfg.data.train : /media/ye/project2/exp/myrk-transformer/data/syl/train
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                       cfg.data.dev : /media/ye/project2/exp/myrk-transformer/data/syl/dev
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                      cfg.data.test : /media/ye/project2/exp/myrk-transformer/data/syl/test
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                     cfg.data.level : word
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                 cfg.data.lowercase : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -           cfg.data.max_sent_length : 50
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.data.src_voc_min_freq : 0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.data.src_voc_limit : 100000
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.data.trg_voc_min_freq : 0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.data.trg_voc_limit : 100000
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -              cfg.testing.beam_size : 10
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                  cfg.testing.alpha : 1.0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.reset_best_ckpt : False
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.reset_scheduler : False
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.reset_optimizer : False
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -           cfg.training.random_seed : 42
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.training.optimizer : adam
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -         cfg.training.learning_rate : 0.0003
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -     cfg.training.learning_rate_min : 5e-07
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.training.weight_decay : 0.0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -        cfg.training.clip_grad_norm : 1.0
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -            cfg.training.batch_size : 80
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -            cfg.training.scheduling : plateau
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -              cfg.training.patience : 10
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.decrease_factor : 0.5
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers - cfg.training.early_stopping_metric : eval_metric
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -                cfg.training.epochs : 30
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.validation_freq : 1000
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -          cfg.training.logging_freq : 100
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -           cfg.training.eval_metric : bleu
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.training.model_dir : models/wmt_myrk_default
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -             cfg.training.overwrite : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -               cfg.training.shuffle : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -              cfg.training.use_cuda : True
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -     cfg.training.max_output_length : 100
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -     cfg.training.print_valid_sents : [0, 1, 2]
2022-02-27 12:35:37,361 - INFO - joeynmt.helpers -       cfg.training.keep_last_ckpts : 5
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -         cfg.model.encoder.rnn_type : lstm
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.embedding_dim : 4096
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.encoder.embeddings.scale : False
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -      cfg.model.encoder.hidden_size : 1000
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -    cfg.model.encoder.bidirectional : True
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -          cfg.model.encoder.dropout : 0.2
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -       cfg.model.encoder.num_layers : 1
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -         cfg.model.decoder.rnn_type : lstm
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.embedding_dim : 4096
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - cfg.model.decoder.embeddings.scale : False
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -        cfg.model.decoder.emb_scale : False
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -      cfg.model.decoder.hidden_size : 1000
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -          cfg.model.decoder.dropout : 0.2
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -   cfg.model.decoder.hidden_dropout : 0.2
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -       cfg.model.decoder.num_layers : 1
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -    cfg.model.decoder.input_feeding : True
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -      cfg.model.decoder.init_hidden : bridge
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers -        cfg.model.decoder.attention : bahdanau
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - Data set sizes: 
	train 15535,
	valid 1000,
	test 1811
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - First training example:
	[SRC] မင်း အဲ့ ဒါ ကို အ ခြား တစ် ခု နဲ့ မ ချိတ် ဘူး လား ။
	[TRG] မင်း ယင်း ချင့် ကို အ ခြား တစ် ခု နန့် မ ချိတ် ပါ လား ။
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - First 10 words (src): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) မ (6) အ (7) ကို (8) တယ် (9) သူ
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - First 10 words (trg): (0) <unk> (1) <pad> (2) <s> (3) </s> (4) ။ (5) အ (6) ကို (7) ရေ (8) မ (9) ပါ
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - Number of Src words (types): 1580
2022-02-27 12:35:37,362 - INFO - joeynmt.helpers - Number of Trg words (types): 1687
2022-02-27 12:35:37,362 - INFO - joeynmt.training - Model(
	encoder=RecurrentEncoder(LSTM(4096, 1000, batch_first=True, bidirectional=True)),
	decoder=RecurrentDecoder(rnn=LSTM(5096, 1000, batch_first=True), attention=BahdanauAttention),
	src_embed=Embeddings(embedding_dim=4096, vocab_size=1580),
	trg_embed=Embeddings(embedding_dim=4096, vocab_size=1687))
2022-02-27 12:35:37,363 - INFO - joeynmt.training - Train stats:
	device: cuda
	n_gpu: 2
	16-bits training: False
	gradient accumulation: 1
	batch size per device: 40
	total batch size (w. parallel & accumulation): 80
2022-02-27 12:35:37,363 - INFO - joeynmt.training - EPOCH 1
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:694: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, batch_sizes, hx, self._flat_weights, self.bias,
/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py:691: UserWarning: RNN module weights are not part of single contiguous chunk of memory. This means they need to be compacted at every call, possibly greatly increasing memory usage. To compact weights again call flatten_parameters(). (Triggered internally at  ../aten/src/ATen/native/cudnn/RNN.cpp:925.)
  result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 48, in <module>
    main()
  File "/home/ye/exp/joeynmt/joeynmt/__main__.py", line 35, in main
    train(cfg_file=args.config_path, skip_test=args.skip_test)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 846, in train
    trainer.train_and_validate(train_data=train_data, valid_data=dev_data)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 447, in train_and_validate
    batch_loss += self._train_step(batch)
  File "/home/ye/exp/joeynmt/joeynmt/training.py", line 539, in _train_step
    batch_loss, _, _, _ = self.model(return_type="loss", **vars(batch))
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 168, in forward
    outputs = self.parallel_apply(replicas, inputs, kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 178, in parallel_apply
    return parallel_apply(replicas, inputs, kwargs, self.device_ids[:len(replicas)])
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 86, in parallel_apply
    output.reraise()
  File "/home/ye/.local/lib/python3.8/site-packages/torch/_utils.py", line 434, in reraise
    raise exception
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 98.00 MiB (GPU 1; 3.95 GiB total capacity; 3.00 GiB already allocated; 97.94 MiB free; 3.14 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m12.427s
user	0m6.328s
sys	0m2.620s
(joey) ye@:~/exp/joeynmt$ 
```

အထက်ပါအတိုင်း out of memory error တက်တယ်။  
အဲဒါကြောင့် hidden_size ကို 600 (100 ပဲ တိုးခဲ့) ပဲထားပြီး beam size ကိုတော့ 10 ပဲ ထားပြီး ထပ် training လုပ်ကြည့်ခဲ့...  

```
       hidden_size: 600
       beam_size: 10 # original setting is 5       
```

training again ... 

```
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 52.00 MiB (GPU 1; 3.95 GiB total capacity; 2.94 GiB already allocated; 40.94 MiB free; 3.18 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m39.949s
user	0m39.533s
sys	0m8.476s
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါအတိုင်း error ပေးပြီး training ရပ်သွားလို့... beam size ကိုလျှော့ပြီး ပြန် train လုပ်ကြည့်ခဲ့...  

```
       hidden_size: 600
       
testing:
    beam_size: 5 # original setting is 5
```

training လုပ်ခဲ့....  

```
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 168, in forward
    outputs = self.parallel_apply(replicas, inputs, kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/data_parallel.py", line 178, in parallel_apply
    return parallel_apply(replicas, inputs, kwargs, self.device_ids[:len(replicas)])
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 86, in parallel_apply
    output.reraise()
  File "/home/ye/.local/lib/python3.8/site-packages/torch/_utils.py", line 434, in reraise
    raise exception
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 52.00 MiB (GPU 1; 3.95 GiB total capacity; 2.94 GiB already allocated; 40.94 MiB free; 3.18 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m38.592s
user	0m40.241s
sys	0m8.479s
(joey) ye@:~/exp/joeynmt$ 
```

လက်ရှိ စက်နဲ့က မနိုင်ဘူး... 
အဲဒါကြောင့် ... နောက်ထပ် အရေးကြီးတဲ့ parameter တစ်ခု ဖြစ်တဲ့ hidden layer ကိုပဲ တိုးကြည့်မယ်။  

```
        num_layers: 2 # 1 ကနေ 2 အထိ တင်ကြည့်ခဲ့...  
```

run ကြည့်ခဲ့...  

```
RuntimeError: Caught RuntimeError in replica 1 on device 1.
Original Traceback (most recent call last):
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/parallel/parallel_apply.py", line 61, in _worker
    output = module(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 84, in forward
    out, _, _, _ = self._encode_decode(**kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 132, in _encode_decode
    return self._decode(encoder_output=encoder_output,
  File "/home/ye/exp/joeynmt/joeynmt/model.py", line 169, in _decode
    return self.decoder(trg_embed=self.trg_embed(trg_input),
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 374, in forward
    prev_att_vector, hidden, att_prob = self._forward_step(
  File "/home/ye/exp/joeynmt/joeynmt/decoders.py", line 249, in _forward_step
    _, hidden = self.rnn(rnn_input, hidden)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ye/.local/lib/python3.8/site-packages/torch/nn/modules/rnn.py", line 691, in forward
    result = _VF.lstm(input, hx, self._flat_weights, self.bias, self.num_layers,
RuntimeError: CUDA out of memory. Tried to allocate 50.00 MiB (GPU 1; 3.95 GiB total capacity; 2.95 GiB already allocated; 16.94 MiB free; 3.21 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF


real	0m38.850s
user	0m40.468s
sys	0m8.179s
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါအတိုင်း error ပေးတယ်။ ဒီတစ်ခါတော့ hidden layer ကို 2 ထားထားပြီး hidden_size ကို 300 ထားကြည့်မယ်...  

```
        num_layers: 2
        hidden_size: 300 # for both encoder/decoder        
```

training လုပ်ကြည့်ခဲ့...  

```
2022-02-27 13:56:56,670 - INFO - joeynmt.training - EPOCH 28
2022-02-27 13:57:16,583 - INFO - joeynmt.training - Epoch  28, Step:     5300, Batch Loss:     0.835923, Tokens per Sec:     1914, Lr: 0.000300
2022-02-27 13:58:12,621 - INFO - joeynmt.training - Epoch  28, Step:     5400, Batch Loss:     1.400406, Tokens per Sec:     1929, Lr: 0.000300
2022-02-27 13:58:45,413 - INFO - joeynmt.training - Epoch  28: total training loss 210.51
2022-02-27 13:58:45,414 - INFO - joeynmt.training - EPOCH 29
2022-02-27 13:59:07,497 - INFO - joeynmt.training - Epoch  29, Step:     5500, Batch Loss:     0.650256, Tokens per Sec:     1963, Lr: 0.000300
2022-02-27 14:00:05,073 - INFO - joeynmt.training - Epoch  29, Step:     5600, Batch Loss:     1.080434, Tokens per Sec:     1886, Lr: 0.000300
2022-02-27 14:00:34,237 - INFO - joeynmt.training - Epoch  29: total training loss 192.59
2022-02-27 14:00:34,237 - INFO - joeynmt.training - EPOCH 30
2022-02-27 14:00:59,486 - INFO - joeynmt.training - Epoch  30, Step:     5700, Batch Loss:     1.102342, Tokens per Sec:     1918, Lr: 0.000300
2022-02-27 14:01:54,616 - INFO - joeynmt.training - Epoch  30, Step:     5800, Batch Loss:     0.951962, Tokens per Sec:     1966, Lr: 0.000300
2022-02-27 14:02:22,152 - INFO - joeynmt.training - Epoch  30: total training loss 179.17
2022-02-27 14:02:22,152 - INFO - joeynmt.training - Training ended after  30 epochs.
2022-02-27 14:02:22,152 - INFO - joeynmt.training - Best validation result (greedy) at step     5000:  82.33 eval_metric.
2022-02-27 14:02:22,170 - INFO - joeynmt.prediction - Process device: cuda, n_gpu: 2, batch_size per device: 40
2022-02-27 14:02:22,171 - INFO - joeynmt.prediction - Loading model from models/wmt_myrk_default/5000.ckpt
2022-02-27 14:02:22,576 - INFO - joeynmt.model - Building an encoder-decoder model...
2022-02-27 14:02:22,862 - INFO - joeynmt.model - Enc-dec model built.
2022-02-27 14:02:22,917 - INFO - joeynmt.prediction - Decoding on dev set (/media/ye/project2/exp/myrk-transformer/data/syl/dev.rk)...
2022-02-27 14:02:54,819 - INFO - joeynmt.prediction -  dev bleu[13a]:  82.53 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 14:02:54,821 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.dev
2022-02-27 14:02:54,821 - INFO - joeynmt.prediction - Decoding on test set (/media/ye/project2/exp/myrk-transformer/data/syl/test.rk)...
2022-02-27 14:03:51,285 - INFO - joeynmt.prediction - test bleu[13a]:  81.19 [Beam search decoding with beam size = 5 and alpha = 1.0]
2022-02-27 14:03:51,289 - INFO - joeynmt.prediction - Translations saved to: models/wmt_myrk_default/00005000.hyps.test

real	58m25.911s
user	71m45.595s
sys	9m6.336s
(joey) ye@:~/exp/joeynmt$ cat ./models/wmt_myrk_default/validations.txt 
Steps: 1000	Loss: 19013.80859	PPL: 4.03538	bleu: 14.87704	LR: 0.00030000	*
Steps: 2000	Loss: 7608.55371	PPL: 1.74763	bleu: 58.67979	LR: 0.00030000	*
Steps: 3000	Loss: 3492.30786	PPL: 1.29206	bleu: 79.77457	LR: 0.00030000	*
Steps: 4000	Loss: 3101.71558	PPL: 1.25556	bleu: 81.94242	LR: 0.00030000	*
Steps: 5000	Loss: 3153.44263	PPL: 1.26033	bleu: 82.32911	LR: 0.00030000	*
(joey) ye@:~/exp/joeynmt$ 

```

အထက်ပါ မော်ဒယ်လည်း သုံးလို့ ရလိမ့်မယ်။  
backup ကူးထားခဲ့...  

