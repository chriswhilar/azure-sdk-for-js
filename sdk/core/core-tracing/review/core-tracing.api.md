## API Report File for "@azure/core-tracing"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts

import { Span as OpenCensusSpan } from '@opencensus/web-types';
import { Tracer as OpenCensusTracer } from '@opencensus/web-types';
import { TracerBase } from '@opencensus/web-types';

// @public
export interface Attributes {
    [attributeKey: string]: unknown;
}

// @public
export interface BinaryFormat {
    fromBytes(buffer: ArrayBuffer): SpanContext | null;
    toBytes(spanContext: SpanContext): ArrayBuffer;
}

// @public
export enum CanonicalCode {
    ABORTED = 10,
    ALREADY_EXISTS = 6,
    CANCELLED = 1,
    DATA_LOSS = 15,
    DEADLINE_EXCEEDED = 4,
    FAILED_PRECONDITION = 9,
    INTERNAL = 13,
    INVALID_ARGUMENT = 3,
    NOT_FOUND = 5,
    OK = 0,
    OUT_OF_RANGE = 11,
    PERMISSION_DENIED = 7,
    RESOURCE_EXHAUSTED = 8,
    UNAUTHENTICATED = 16,
    UNAVAILABLE = 14,
    UNIMPLEMENTED = 12,
    UNKNOWN = 2
}

// @public
export interface Event {
    attributes?: Attributes;
    name: string;
}

// @public
export function extractSpanContextFromTraceParentHeader(traceParentHeader: string): SpanContext | undefined;

// @public
export function getTraceParentHeader(spanContext: SpanContext): string | undefined;

// @public
export function getTracer(): Tracer;

// @public
export type HrTime = [number, number];

// @public
export interface HttpTextFormat {
    extract(format: string, carrier: unknown): SpanContext | null;
    inject(spanContext: SpanContext, format: string, carrier: unknown): void;
}

// @public
export interface Link {
    attributes?: Attributes;
    spanContext: SpanContext;
}

// @public
export class NoOpSpan implements Span {
    addEvent(_name: string, _attributes?: Attributes): this;
    addLink(_spanContext: SpanContext, _attributes?: Attributes): this;
    context(): SpanContext;
    end(_endTime?: number): void;
    isRecordingEvents(): boolean;
    setAttribute(_key: string, _value: unknown): this;
    setAttributes(_attributes: Attributes): this;
    setStatus(_status: Status): this;
    updateName(_name: string): this;
}

// @public
export class NoOpTracer implements Tracer {
    bind<T>(target: T, _span?: Span): T;
    getBinaryFormat(): BinaryFormat;
    getCurrentSpan(): Span;
    getHttpTextFormat(): HttpTextFormat;
    recordSpanData(_span: Span): void;
    startSpan(_name: string, _options?: SpanOptions): Span;
    withSpan<T extends (...args: unknown[]) => ReturnType<T>>(_span: Span, fn: T): ReturnType<T>;
}

export { OpenCensusSpan }

// @public
export class OpenCensusSpanWrapper implements Span {
    constructor(span: OpenCensusSpan);
    constructor(tracer: OpenCensusTracerWrapper, name: string, options?: SpanOptions);
    addEvent(name: string, attributes?: Attributes): this;
    addLink(spanContext: SpanContext, attributes?: Attributes): this;
    context(): SpanContext;
    end(_endTime?: number): void;
    getWrappedSpan(): OpenCensusSpan;
    isRecordingEvents(): boolean;
    setAttribute(key: string, value: unknown): this;
    setAttributes(attributes: Attributes): this;
    setStatus(status: Status): this;
    updateName(name: string): this;
}

export { OpenCensusTracer }

// @public
export class OpenCensusTracerWrapper implements Tracer {
    constructor(tracer: TracerBase);
    bind<T>(target: T, span?: Span): T;
    getBinaryFormat(): BinaryFormat;
    getCurrentSpan(): Span | null;
    getHttpTextFormat(): HttpTextFormat;
    getWrappedTracer(): TracerBase;
    recordSpanData(span: Span): void;
    startSpan(name: string, options?: SpanOptions): Span;
    withSpan<T extends (...args: unknown[]) => unknown>(span: Span, fn: T): ReturnType<T>;
}

// @public
export interface Sampler {
    shouldSample(parentContext?: SpanContext): boolean;
    toString(): string;
}

// @public
export function setTracer(tracer: Tracer): void;

// @public
export interface Span {
    addEvent(name: string, attributes?: Attributes): this;
    addLink(spanContext: SpanContext, attributes?: Attributes): this;
    context(): SpanContext;
    end(endTime?: TimeInput): void;
    isRecordingEvents(): boolean;
    setAttribute(key: string, value: unknown): this;
    setAttributes(attributes: Attributes): this;
    setStatus(status: Status): this;
    updateName(name: string): this;
}

// @public
export interface SpanContext {
    spanId: string;
    traceFlags?: TraceFlags;
    traceId: string;
    traceState?: TraceState;
}

// @public
export interface SpanGraph {
    roots: SpanGraphNode[];
}

// @public
export interface SpanGraphNode {
    children: SpanGraphNode[];
    name: string;
}

// @public
export enum SpanKind {
    CLIENT = 2,
    CONSUMER = 4,
    INTERNAL = 0,
    PRODUCER = 3,
    SERVER = 1
}

// @public
export interface SpanOptions {
    attributes?: Attributes;
    isRecordingEvents?: boolean;
    kind?: SpanKind;
    parent?: Span | SpanContext;
    startTime?: number;
}

// @public
export interface Status {
    code: CanonicalCode;
    message?: string;
}

// @public
export class TestSpan extends NoOpSpan {
    constructor(parentTracer: TestTracer, name: string, context: SpanContext, kind: SpanKind, parentSpanId?: string, startTime?: TimeInput);
    context(): SpanContext;
    end(_endTime?: number): void;
    endCalled: boolean;
    isRecordingEvents(): boolean;
    kind: SpanKind;
    name: string;
    readonly parentSpanId?: string;
    setStatus(status: Status): this;
    readonly startTime: TimeInput;
    status: Status;
    tracer(): Tracer;
    }

// @public
export class TestTracer extends NoOpTracer {
    getActiveSpans(): TestSpan[];
    getKnownSpans(): TestSpan[];
    getRootSpans(): TestSpan[];
    getSpanGraph(traceId: string): SpanGraph;
    startSpan(name: string, options?: SpanOptions): TestSpan;
    }

// @public
export interface TimedEvent extends Event {
    time: HrTime;
}

// @public
export type TimeInput = HrTime | number | Date;

// @public
export enum TraceFlags {
    SAMPLED = 1,
    UNSAMPLED = 0
}

// @public
export interface Tracer {
    bind<T>(target: T, span?: Span): T;
    getBinaryFormat(): BinaryFormat;
    getCurrentSpan(): Span | null;
    getHttpTextFormat(): HttpTextFormat;
    recordSpanData(span: Span): void;
    startSpan(name: string, options?: SpanOptions): Span;
    withSpan<T extends (...args: unknown[]) => ReturnType<T>>(span: Span, fn: T): ReturnType<T>;
}

// @public
export interface TraceState {
    get(key: string): string | undefined;
    serialize(): string;
    set(key: string, value: string): void;
    unset(key: string): void;
}


// (No @packageDocumentation comment for this package)

```