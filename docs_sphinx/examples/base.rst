Simple Examples
===============

Following pieces of code show an example of Fitter class calls with possible inputs.


TraceFitter
------------

.. code:: python

  n_opt = NevergradOptimizer(method='PSO')
  metric = MSEMetric()

  fitter = TraceFitter(model=model,
                        input_var='I',
                        output_var='v',
                        input=inp_trace,
                        dt=0.1*ms,
                        method='exponential_euler',
                        output=out_trace,
                        n_samples=5,)

  results, error = fitter.fit(optimizer=n_opt,
                              metric=metric,
                              callback=True,
                              n_rounds=1,
                              param_init={'v': -65*mV},
                              gl=[1e-8*siemens*cm**-2 * area, 1e-3*siemens*cm**-2 * area],
                              g_na=[1*msiemens*cm**-2 * area, 2000*msiemens*cm**-2 * area],
                              g_kd=[1*msiemens*cm**-2 * area, 1000*msiemens*cm**-2 * area],)



SpikeFitter
-----------

.. code:: python

  n_opt = SkoptOptimizer('DE')
  metric = GammaFactor(dt, 60*ms)

  fitter = TraceFitter(model=eqs,
                       input_var='I',
                       dt=0.1*ms,
                       input=inp_traces,
                       output=out_spikes,
                       n_samples=30,
                       threshold='v > -50*mV',
                       reset='v = -70*mV',
                       method='exponential_euler',)

  results, error = fitter.fit(n_rounds=2,
                   optimizer=n_opt,
                   metric=metric,
                   param_init={'v': -70*mV},
                   gL=[20*nS, 40*nS],
                   C = [0.5*nF, 1.5*nF])