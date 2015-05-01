#!/usr/bin/env ruby

def clocks
  %w(🕛 🕐 🕑 🕒 🕓 🕔 🕕 🕖 🕗 🕘 🕙 🕚)
end

def spin_during
  working = 0
  timer   = Thread.new do
    while working do
      clock_index = (working+=1) % clocks.length
      $stdout.write "#{clocks[clock_index]} "
      sleep 0.1
      $stdout.write "\b\b"
    end
  end

  if block_given?
    yield.tap do
      working = false
      timer.join
    end
  end
end

if $stdout.tty? && !ARGV.empty?
  $stdout.write spin_during { %x(#{ARGV.join(' ')}) }
else
  spin_during
  $stdout.write "\b\b#{ARGF.read}"
end
