project('ODAS', 'c', license : 'GPL3+', default_options : ['default_library=shared'])

cc = meson.get_compiler('c')
pkg = import('pkgconfig')

fftw3_dep = dependency('fftw3f')
alsa_dep = dependency('alsa')
libconfig_dep = dependency('libconfig')

thread_dep = dependency('threads')
libm_dep = cc.find_library('m', required : false)

topinc = include_directories('include')
odasinc = include_directories('include/odas')
subdir ('include')

src = ['src/general/format.c', 'src/general/interface.c', 'src/general/link.c',
    'src/general/mic.c', 'src/general/samplerate.c', 'src/general/soundspeed.c',
    'src/general/spatialfilter.c', 'src/general/thread.c', 'src/init/combining.c',
    'src/init/delay.c', 'src/init/directivity.c', 'src/init/hit.c',
    'src/init/linking.c', 'src/init/scanning.c', 'src/init/space.c',
    'src/init/windowing.c', 'src/signal/acorr.c', 'src/signal/aimg.c',
    'src/signal/area.c', 'src/signal/assignation.c', 'src/signal/beampattern.c',
    'src/signal/category.c', 'src/signal/coherence.c', 'src/signal/delta.c',
    'src/signal/demixing.c', 'src/signal/env.c', 'src/signal/frame.c',
    'src/signal/freq.c', 'src/signal/gain.c', 'src/signal/hop.c', 'src/signal/index.c',
    'src/signal/kalman.c', 'src/signal/map.c', 'src/signal/mask.c', 'src/signal/mixture.c',
    'src/signal/pair.c', 'src/signal/particle.c', 'src/signal/pitch.c',
    'src/signal/point.c', 'src/signal/postprob.c', 'src/signal/pot.c',
    'src/signal/scan.c', 'src/signal/spatialgain.c', 'src/signal/spatialindex.c',
    'src/signal/spatialmask.c', 'src/signal/steer.c', 'src/signal/target.c',
    'src/signal/tau.c', 'src/signal/tdoa.c', 'src/signal/track.c',
    'src/signal/triangle.c', 'src/signal/window.c', 'src/signal/xcorr.c',
    'src/system/acorr2pitch.c', 'src/system/demixing2env.c',
    'src/system/demixing2freq.c', 'src/system/env2env.c', 'src/system/hop2hop.c',
    'src/system/hop2frame.c', 'src/system/frame2freq.c', 'src/system/freq2acorr.c',
    'src/system/freq2env.c', 'src/system/freq2freq.c', 'src/system/freq2frame.c',
    'src/system/freq2xcorr.c', 'src/system/frame2hop.c', 'src/system/gain2mask.c',
    'src/system/kalman2coherence.c', 'src/system/kalman2kalman.c',
    'src/system/mixture2mixture.c', 'src/system/particle2coherence.c',
    'src/system/particle2particle.c', 'src/system/pitch2category.c',
    'src/system/steer2demixing.c', 'src/system/track2gain.c',
    'src/system/track2steer.c', 'src/system/xcorr2aimg.c',
    'src/system/xcorr2xcorr.c', 'src/utils/cmatrix.c', 'src/utils/fft.c',
    'src/utils/fifo.c', 'src/utils/gaussian.c', 'src/utils/gaussjordan.c',
    'src/utils/inverse.c', 'src/utils/matrix.c', 'src/utils/pcm.c',
    'src/utils/random.c', 'src/utils/transcendental.c',
    'src/aconnector/acon_categories.c', 'src/aconnector/acon_hops.c',
    'src/aconnector/acon_pots.c', 'src/aconnector/acon_powers.c',
    'src/aconnector/acon_spectra.c', 'src/aconnector/acon_targets.c',
    'src/aconnector/acon_tracks.c', 'src/ainjector/ainj_targets.c',
    'src/amessage/amsg_categories.c', 'src/amessage/amsg_hops.c',
    'src/amessage/amsg_pots.c', 'src/amessage/amsg_powers.c',
    'src/amessage/amsg_spectra.c', 'src/amessage/amsg_targets.c',
    'src/amessage/amsg_tracks.c', 'src/amodule/amod_classify.c',
    'src/amodule/amod_istft.c', 'src/amodule/amod_mapping.c',
    'src/amodule/amod_noise.c', 'src/amodule/amod_resample.c',
    'src/amodule/amod_ssl.c', 'src/amodule/amod_sss.c',
    'src/amodule/amod_sst.c', 'src/amodule/amod_stft.c', 'src/amodule/amod_volume.c',
    'src/asink/asnk_categories.c', 'src/asink/asnk_hops.c', 'src/asink/asnk_pots.c',
    'src/asink/asnk_powers.c', 'src/asink/asnk_spectra.c', 'src/asink/asnk_tracks.c',
    'src/asource/asrc_hops.c', 'src/connector/con_categories.c',
    'src/connector/con_hops.c', 'src/connector/con_pots.c',
    'src/connector/con_powers.c', 'src/connector/con_spectra.c',
    'src/connector/con_targets.c', 'src/connector/con_tracks.c',
    'src/injector/inj_targets.c', 'src/message/msg_categories.c',
    'src/message/msg_hops.c', 'src/message/msg_pots.c', 'src/message/msg_powers.c',
    'src/message/msg_spectra.c', 'src/message/msg_targets.c',
    'src/message/msg_tracks.c', 'src/module/mod_classify.c', 'src/module/mod_istft.c',
    'src/module/mod_mapping.c', 'src/module/mod_noise.c', 'src/module/mod_resample.c',
    'src/module/mod_ssl.c', 'src/module/mod_sss.c', 'src/module/mod_sst.c',
    'src/module/mod_stft.c', 'src/module/mod_volume.c', 'src/sink/snk_categories.c',
    'src/sink/snk_hops.c', 'src/sink/snk_pots.c', 'src/sink/snk_powers.c',
    'src/sink/snk_spectra.c', 'src/sink/snk_tracks.c', 'src/source/src_hops.c']

odas_lib = library('odas', src, install: true, include_directories : odasinc, dependencies : [ fftw3_dep, alsa_dep, thread_dep, libm_dep ])
pkg.generate(odas_lib, subdirs: 'odas')

odas_live_src = [ 'demo/odaslive/main.c', 'demo/odaslive/configs.c', 'demo/odaslive/objects.c', 'demo/odaslive/parameters.c', 'demo/odaslive/profiler.c', 'demo/odaslive/threads.c' ]

odaslive_exe = executable('odaslive', odas_live_src, include_directories : [topinc, odasinc], dependencies: [libconfig_dep, libm_dep], link_with : odas_lib)

odasserver_exe = executable('odasserver', 'demo/odasserver/main.c', include_directories : [topinc, odasinc], link_with : odas_lib)

